---
title: "Application Insights'ta uyarıları ayarlamak için PowerShell kullanma | Microsoft Docs"
description: "Ölçüm değişiklikler hakkında e-postaları almak için Application Insights yapılandırmasını otomatikleştirin."
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
ms.openlocfilehash: 64675c51abf80daa3a55220f910aa8fdee1042ca
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="use-powershell-to-set-alerts-in-application-insights"></a><span data-ttu-id="0f3d8-103">Application Insights uyarıları ayarlamak için PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="0f3d8-103">Use PowerShell to set alerts in Application Insights</span></span>
<span data-ttu-id="0f3d8-104">Yapılandırmasını otomatikleştirebilirsiniz [uyarıları](app-insights-alerts.md) içinde [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0f3d8-104">You can automate the configuration of [alerts](app-insights-alerts.md) in [Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="0f3d8-105">Buna ek olarak, şunları yapabilirsiniz [ayarlamak yanıtınız bir uyarıya otomatik hale getirmek için Web kancası](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="0f3d8-105">In addition, you can [set webhooks to automate your response to an alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0f3d8-106">Aynı anda kaynakları ve Uyarıları oluşturmak istiyorsanız, göz önünde bulundurun [bir Azure Resource Manager şablonu kullanarak](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0f3d8-106">If you want to create resources and alerts at the same time, consider [using an Azure Resource Manager template](app-insights-powershell.md).</span></span>
>
>

## <a name="one-time-setup"></a><span data-ttu-id="0f3d8-107">Tek seferlik Kurulumu</span><span class="sxs-lookup"><span data-stu-id="0f3d8-107">One-time setup</span></span>
<span data-ttu-id="0f3d8-108">Önce Azure aboneliğinizle PowerShell kullanmadıysanız:</span><span class="sxs-lookup"><span data-stu-id="0f3d8-108">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="0f3d8-109">Komut dosyalarını çalıştırmak istediğiniz Azure Powershell modülünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-109">Install the Azure Powershell module on the machine where you want to run the scripts.</span></span>

* <span data-ttu-id="0f3d8-110">Yükleme [Microsoft Web Platformu Yükleyicisi (v5 veya üzeri)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f3d8-110">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="0f3d8-111">Microsoft Azure PowerShell'i yüklemek için kullanın</span><span class="sxs-lookup"><span data-stu-id="0f3d8-111">Use it to install Microsoft Azure Powershell</span></span>

## <a name="connect-to-azure"></a><span data-ttu-id="0f3d8-112">Azure'a Bağlanma</span><span class="sxs-lookup"><span data-stu-id="0f3d8-112">Connect to Azure</span></span>
<span data-ttu-id="0f3d8-113">Azure PowerShell'i başlatın ve [aboneliğinize bağlanma](/powershell/azure/overview):</span><span class="sxs-lookup"><span data-stu-id="0f3d8-113">Start Azure PowerShell and [connect to your subscription](/powershell/azure/overview):</span></span>

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a><span data-ttu-id="0f3d8-114">Uyarıları alma</span><span class="sxs-lookup"><span data-stu-id="0f3d8-114">Get alerts</span></span>
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a><span data-ttu-id="0f3d8-115">Uyarı ekleme</span><span class="sxs-lookup"><span data-stu-id="0f3d8-115">Add alert</span></span>
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



## <a name="example-1"></a><span data-ttu-id="0f3d8-116">Örnek 1</span><span class="sxs-lookup"><span data-stu-id="0f3d8-116">Example 1</span></span>
<span data-ttu-id="0f3d8-117">Sunucu yanıtı üzerinde 5 dakika ortalaması HTTP isteklerine 1 saniyeden daha yavaş ise bana e-posta.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-117">Email me if the server's response to HTTP requests, averaged over 5 minutes, is slower than 1 second.</span></span> <span data-ttu-id="0f3d8-118">My Application Insights kaynağı IceCreamWebApp denir ve Fabrikam kaynak grubunda bulunuyor.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-118">My Application Insights resource is called IceCreamWebApp, and it is in resource group Fabrikam.</span></span> <span data-ttu-id="0f3d8-119">Azure aboneliğinin sahibi ben.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-119">I am the owner of the Azure subscription.</span></span>

<span data-ttu-id="0f3d8-120">Abonelik kimliği (değil uygulamanın izleme anahtarı) GUID'dir.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-120">The GUID is the subscription ID (not the instrumentation key of the application).</span></span>

    Add-AlertRule -Name "slow responses" `
     -Description "email me if the server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a><span data-ttu-id="0f3d8-121">Örnek 2</span><span class="sxs-lookup"><span data-stu-id="0f3d8-121">Example 2</span></span>
<span data-ttu-id="0f3d8-122">Bir uygulama içinde kullanmam sahip [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) "salesPerHour." adlı bir ölçüm bildirmek için</span><span class="sxs-lookup"><span data-stu-id="0f3d8-122">I have an application in which I use [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) to report a metric named "salesPerHour."</span></span> <span data-ttu-id="0f3d8-123">"SalesPerHour" 100 düşerse bir e-posta my arkadaşlarınıza üzerinde 24 saat ortalaması gönderin.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-123">Send an email to my colleagues if "salesPerHour" drops below 100, averaged over 24 hours.</span></span>

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

<span data-ttu-id="0f3d8-124">Aynı kural kullanılarak bildirilen ölçümü için kullanılabilir [ölçüm parametresi](app-insights-api-custom-events-metrics.md#properties) TrackEvent veya trackPageView gibi başka bir izleme çağrısı.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-124">The same rule can be used for the metric reported by using the [measurement parameter](app-insights-api-custom-events-metrics.md#properties) of another tracking call such as TrackEvent or trackPageView.</span></span>

## <a name="metric-names"></a><span data-ttu-id="0f3d8-125">Ölçüm adları</span><span class="sxs-lookup"><span data-stu-id="0f3d8-125">Metric names</span></span>
| <span data-ttu-id="0f3d8-126">Ölçüm adı</span><span class="sxs-lookup"><span data-stu-id="0f3d8-126">Metric name</span></span> | <span data-ttu-id="0f3d8-127">Ekran adı</span><span class="sxs-lookup"><span data-stu-id="0f3d8-127">Screen name</span></span> | <span data-ttu-id="0f3d8-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0f3d8-128">Description</span></span> |
| --- | --- | --- |
| `basicExceptionBrowser.count` |<span data-ttu-id="0f3d8-129">Tarayıcı özel durumları</span><span class="sxs-lookup"><span data-stu-id="0f3d8-129">Browser exceptions</span></span> |<span data-ttu-id="0f3d8-130">Tarayıcıda oluşturulan Yakalanmayan Özel durumların sayısı.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-130">Count of uncaught exceptions thrown in the browser.</span></span> |
| `basicExceptionServer.count` |<span data-ttu-id="0f3d8-131">Sunucu özel durumları</span><span class="sxs-lookup"><span data-stu-id="0f3d8-131">Server exceptions</span></span> |<span data-ttu-id="0f3d8-132">Uygulama tarafından oluşturulan işlenmemiş özel durum sayısı</span><span class="sxs-lookup"><span data-stu-id="0f3d8-132">Count of unhandled exceptions thrown by the app</span></span> |
| `clientPerformance.clientProcess.value` |<span data-ttu-id="0f3d8-133">İstemci işlem süresi</span><span class="sxs-lookup"><span data-stu-id="0f3d8-133">Client processing time</span></span> |<span data-ttu-id="0f3d8-134">DOM yüklenene kadar belgeyi son baytını alma arasındaki süre.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-134">Time between receiving the last byte of a document until the DOM is loaded.</span></span> <span data-ttu-id="0f3d8-135">Zaman uyumsuz isteği hala işliyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-135">Async requests may still be processing.</span></span> |
| `clientPerformance.networkConnection.value` |<span data-ttu-id="0f3d8-136">Sayfa yükleme ağ bağlantı süresi</span><span class="sxs-lookup"><span data-stu-id="0f3d8-136">Page load network connect time</span></span> |<span data-ttu-id="0f3d8-137">Tarayıcı ağa bağlanmak için gereken süreyi.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-137">Time the browser takes to connect to the network.</span></span> <span data-ttu-id="0f3d8-138">Önbelleğe alınmış 0 olabilir.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-138">Can be 0 if cached.</span></span> |
| `clientPerformance.receiveRequest.value` |<span data-ttu-id="0f3d8-139">Alıcı yanıt süresi</span><span class="sxs-lookup"><span data-stu-id="0f3d8-139">Receiving response time</span></span> |<span data-ttu-id="0f3d8-140">Yanıt almayı başlatma isteği gönderilirken tarayıcı arasındaki süre.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-140">Time between browser sending request to starting to receive response.</span></span> |
| `clientPerformance.sendRequest.value` |<span data-ttu-id="0f3d8-141">İstek süresi Gönder</span><span class="sxs-lookup"><span data-stu-id="0f3d8-141">Send request time</span></span> |<span data-ttu-id="0f3d8-142">İsteği göndermek için tarayıcı tarafından harcanan süre.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-142">Time taken by browser to send request.</span></span> |
| `clientPerformance.total.value` |<span data-ttu-id="0f3d8-143">Tarayıcı sayfa yükleme süresi</span><span class="sxs-lookup"><span data-stu-id="0f3d8-143">Browser page load time</span></span> |<span data-ttu-id="0f3d8-144">DOM, stil sayfaları, betikler ve görüntüleri yüklenene kadar kullanıcı isteği süresi.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-144">Time from user request until DOM, stylesheets, scripts and images are loaded.</span></span> |
| `performanceCounter.available_bytes.value` |<span data-ttu-id="0f3d8-145">Kullanılabilir bellek</span><span class="sxs-lookup"><span data-stu-id="0f3d8-145">Available memory</span></span> |<span data-ttu-id="0f3d8-146">Bir işlem veya sistem kullanımı için hemen kullanılabilir fiziksel bellek.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-146">Physical memory immediately available for a process or for system use.</span></span> |
| `performanceCounter.io_data_bytes_per_sec.value` |<span data-ttu-id="0f3d8-147">İşlemin g/ç hızı</span><span class="sxs-lookup"><span data-stu-id="0f3d8-147">Process IO Rate</span></span> |<span data-ttu-id="0f3d8-148">Okunabilir ve yazılabilir dosyaları, ağ ve aygıtlar için saniye başına toplam bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-148">Total bytes per second read and written to files, network and devices.</span></span> |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |<span data-ttu-id="0f3d8-149">özel durum oranı</span><span class="sxs-lookup"><span data-stu-id="0f3d8-149">exception rate</span></span> |<span data-ttu-id="0f3d8-150">Saniye başına oluşturulan özel durumları.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-150">Exceptions thrown per second.</span></span> |
| `performanceCounter.percentage_processor_time.value` |<span data-ttu-id="0f3d8-151">İşlem CPU</span><span class="sxs-lookup"><span data-stu-id="0f3d8-151">Process CPU</span></span> |<span data-ttu-id="0f3d8-152">Tüm işlem iş parçacıklarının yönergeleri yürütmek için işlemciyi tarafından uygulamaları işlemi için kullanılan geçen sürenin yüzdesi.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-152">The percentage of elapsed time of all process threads used by the processor to execution instructions for the applications process.</span></span> |
| `performanceCounter.percentage_processor_total.value` |<span data-ttu-id="0f3d8-153">İşlemci zamanı</span><span class="sxs-lookup"><span data-stu-id="0f3d8-153">Processor time</span></span> |<span data-ttu-id="0f3d8-154">İşlemcinin boşta olmayan iş parçacıklarında harcadığı zamanı yüzdesi.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-154">The percentage of time that the processor spends in non-Idle threads.</span></span> |
| `performanceCounter.process_private_bytes.value` |<span data-ttu-id="0f3d8-155">İşlem özel bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="0f3d8-155">Process private bytes</span></span> |<span data-ttu-id="0f3d8-156">Özel olarak izlenen uygulamanın işlemlere atanan bellek.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-156">Memory exclusively assigned to the monitored application's processes.</span></span> |
| `performanceCounter.request_execution_time.value` |<span data-ttu-id="0f3d8-157">ASP.NET isteği yürütme süresi</span><span class="sxs-lookup"><span data-stu-id="0f3d8-157">ASP.NET request execution time</span></span> |<span data-ttu-id="0f3d8-158">En son isteği yürütme süresi.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-158">Execution time of the most recent request.</span></span> |
| `performanceCounter.requests_in_application_queue.value` |<span data-ttu-id="0f3d8-159">ASP.NET isteklerini yürütme kuyruğundaki</span><span class="sxs-lookup"><span data-stu-id="0f3d8-159">ASP.NET requests in execution queue</span></span> |<span data-ttu-id="0f3d8-160">Uygulama istek sırası uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-160">Length of the application request queue.</span></span> |
| `performanceCounter.requests_per_sec.value` |<span data-ttu-id="0f3d8-161">ASP.NET isteği hızı</span><span class="sxs-lookup"><span data-stu-id="0f3d8-161">ASP.NET request rate</span></span> |<span data-ttu-id="0f3d8-162">Saniye başına uygulamaya ASP.NET gelen tüm isteklerin oranı.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-162">Rate of all requests to the application per second from ASP.NET.</span></span> |
| `remoteDependencyFailed.durationMetric.count` |<span data-ttu-id="0f3d8-163">Bağımlılık hataları</span><span class="sxs-lookup"><span data-stu-id="0f3d8-163">Dependency failures</span></span> |<span data-ttu-id="0f3d8-164">Sunucu uygulaması için dış kaynak tarafından yapılan başarısız çağrı sayısı.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-164">Count of failed calls made by the server application to external resources.</span></span> |
| `request.duration` |<span data-ttu-id="0f3d8-165">Sunucu yanıt süresi</span><span class="sxs-lookup"><span data-stu-id="0f3d8-165">Server response time</span></span> |<span data-ttu-id="0f3d8-166">Bir HTTP isteği alma ve yanıtı göndermeyi bitirmeden arasındaki süre.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-166">Time between receiving an HTTP request and finishing sending the response.</span></span> |
| `request.rate` |<span data-ttu-id="0f3d8-167">İstek oranı</span><span class="sxs-lookup"><span data-stu-id="0f3d8-167">Request rate</span></span> |<span data-ttu-id="0f3d8-168">Saniye başına uygulama için tüm istekleri oranı.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-168">Rate of all requests to the application per second.</span></span> |
| `requestFailed.count` |<span data-ttu-id="0f3d8-169">Başarısız istekler</span><span class="sxs-lookup"><span data-stu-id="0f3d8-169">Failed requests</span></span> |<span data-ttu-id="0f3d8-170">Bir yanıt kodu ile sonuçlandı sayısı, HTTP isteklerini > = 400</span><span class="sxs-lookup"><span data-stu-id="0f3d8-170">Count of HTTP requests that resulted in a response code >= 400</span></span> |
| `view.count` |<span data-ttu-id="0f3d8-171">Sayfa görünümleri</span><span class="sxs-lookup"><span data-stu-id="0f3d8-171">Page views</span></span> |<span data-ttu-id="0f3d8-172">Bir web sayfası için istemci kullanıcı isteklerini sayısı.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-172">Count of client user requests for a web page.</span></span> <span data-ttu-id="0f3d8-173">Yapay trafiği filtrelenmelidir.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-173">Synthetic traffic is filtered out.</span></span> |
| <span data-ttu-id="0f3d8-174">{, özel ölçüm adı}</span><span class="sxs-lookup"><span data-stu-id="0f3d8-174">{your custom metric name}</span></span> |<span data-ttu-id="0f3d8-175">{Ölçüm adı}</span><span class="sxs-lookup"><span data-stu-id="0f3d8-175">{Your metric name}</span></span> |<span data-ttu-id="0f3d8-176">Ölçüm değeri tarafından bildirilen [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) veya [izleme çağrı ölçümleri parametresinin](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="0f3d8-176">Your metric value reported by [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) or in the [measurements parameter of a tracking call](app-insights-api-custom-events-metrics.md#properties).</span></span> |

<span data-ttu-id="0f3d8-177">Ölçümleri farklı telemetri modülleri tarafından gönderilir:</span><span class="sxs-lookup"><span data-stu-id="0f3d8-177">The metrics are sent by different telemetry modules:</span></span>

| <span data-ttu-id="0f3d8-178">Ölçüm grubu</span><span class="sxs-lookup"><span data-stu-id="0f3d8-178">Metric group</span></span> | <span data-ttu-id="0f3d8-179">Toplayıcı Modülü</span><span class="sxs-lookup"><span data-stu-id="0f3d8-179">Collector module</span></span> |
| --- | --- |
| <span data-ttu-id="0f3d8-180">basicExceptionBrowser,</span><span class="sxs-lookup"><span data-stu-id="0f3d8-180">basicExceptionBrowser,</span></span><br/><span data-ttu-id="0f3d8-181">clientPerformance,</span><span class="sxs-lookup"><span data-stu-id="0f3d8-181">clientPerformance,</span></span><br/><span data-ttu-id="0f3d8-182">görünüm</span><span class="sxs-lookup"><span data-stu-id="0f3d8-182">view</span></span> |[<span data-ttu-id="0f3d8-183">Tarayıcı JavaScript</span><span class="sxs-lookup"><span data-stu-id="0f3d8-183">Browser JavaScript</span></span>](app-insights-javascript.md) |
| <span data-ttu-id="0f3d8-184">performanceCounter</span><span class="sxs-lookup"><span data-stu-id="0f3d8-184">performanceCounter</span></span> |[<span data-ttu-id="0f3d8-185">Performans</span><span class="sxs-lookup"><span data-stu-id="0f3d8-185">Performance</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="0f3d8-186">remoteDependencyFailed</span><span class="sxs-lookup"><span data-stu-id="0f3d8-186">remoteDependencyFailed</span></span> |[<span data-ttu-id="0f3d8-187">Bağımlılık</span><span class="sxs-lookup"><span data-stu-id="0f3d8-187">Dependency</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="0f3d8-188">isteği</span><span class="sxs-lookup"><span data-stu-id="0f3d8-188">request,</span></span><br/><span data-ttu-id="0f3d8-189">requestFailed</span><span class="sxs-lookup"><span data-stu-id="0f3d8-189">requestFailed</span></span> |[<span data-ttu-id="0f3d8-190">Sunucu isteği</span><span class="sxs-lookup"><span data-stu-id="0f3d8-190">Server request</span></span>](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a><span data-ttu-id="0f3d8-191">Web kancaları</span><span class="sxs-lookup"><span data-stu-id="0f3d8-191">Webhooks</span></span>
<span data-ttu-id="0f3d8-192">Yapabilecekleriniz [bir uyarı yanıtınızı otomatikleştirmek](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="0f3d8-192">You can [automate your response to an alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="0f3d8-193">Bir uyarı ortaya çıktığında azure tercih ettiğiniz bir web adresini çağırır.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-193">Azure will call a web address of your choice when an alert is raised.</span></span>

## <a name="see-also"></a><span data-ttu-id="0f3d8-194">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="0f3d8-194">See also</span></span>
* [<span data-ttu-id="0f3d8-195">Application Insights yapılandırmak için komut dosyası</span><span class="sxs-lookup"><span data-stu-id="0f3d8-195">Script to configure Application Insights</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="0f3d8-196">Application Insights ve web test kaynakları Şablondan Oluştur</span><span class="sxs-lookup"><span data-stu-id="0f3d8-196">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="0f3d8-197">Microsoft Azure tanılama Application Insights'a Kuplaj otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="0f3d8-197">Automate coupling Microsoft Azure Diagnostics to Application Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="0f3d8-198">Bir uyarı yanıtınızı otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="0f3d8-198">Automate your response to an alert</span></span>](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
