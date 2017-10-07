---
title: "aaaStream Azure tanılama günlükleri tooan olay hub'ları Namespace | Microsoft Docs"
description: "Nasıl tooan olay hub'ları ad toostream Azure tanılama günlüklerini öğrenin."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 42bc4845-c564-4568-b72d-0614591ebd80
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: 00092ea8f3fe4fa1476e3a697bf1e8645dd21e6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-azure-diagnostic-logs-tooan-event-hubs-namespace"></a><span data-ttu-id="b4043-103">Azure tanılama günlükleri tooan olay hub'ları Namespace akışı</span><span class="sxs-lookup"><span data-stu-id="b4043-103">Stream Azure Diagnostic Logs tooan Event Hubs Namespace</span></span>
<span data-ttu-id="b4043-104">**[Azure tanılama günlüklerini](monitoring-overview-of-diagnostic-logs.md)**  içinde hello hello Portal içinde yerleşik "TooEvent hub'ları Dışarı Aktar" seçeneğini kullanarak gerçek zamanlı tooany uygulama yakın gönderilebilen ya da hizmet veri yolu kural kimliği'hello Azure PowerShell aracılığıyla tanılama ayarında hello etkinleştirerek Cmdlet'lerini veya Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b4043-104">**[Azure diagnostic logs](monitoring-overview-of-diagnostic-logs.md)** can be streamed in near real time tooany application using hello built-in “Export tooEvent Hubs” option in hello Portal, or by enabling hello Service Bus Rule ID in a diagnostic setting via hello Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a><span data-ttu-id="b4043-105">Tanılama günlüklerini ve olay hub'ları ile yapabilecekleriniz</span><span class="sxs-lookup"><span data-stu-id="b4043-105">What you can do with diagnostics logs and Event Hubs</span></span>
<span data-ttu-id="b4043-106">Yetenek akış için tanılama günlükleri hello kullanabilir birkaç yollar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b4043-106">Here are just a few ways you might use hello streaming capability for Diagnostic Logs:</span></span>

* <span data-ttu-id="b4043-107">**Akış günlükleri too3rd taraf günlüğe kaydetme ve telemetri sistemleri** – zaman içinde olay hub'ları akış hello mekanizması toopipe tanılama günlüklerinize toothird taraf Sıem'lerden duruma ve oturum analiz çözümleri.</span><span class="sxs-lookup"><span data-stu-id="b4043-107">**Stream logs too3rd party logging and telemetry systems** – Over time, Event Hubs streaming will become hello mechanism toopipe your diagnostic logs in toothird-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="b4043-108">**Hizmet durumu "etkin yolunuzda" veri tooPowerBI akış tarafından görüntülemek** – olay hub'ı kullanarak, akış analizi ve Powerbı, Azure hizmetlerinizi toonear gerçek zamanlı Öngörüler tanılama verilerinizi kolayca dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4043-108">**View service health by streaming “hot path” data tooPowerBI** – Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your diagnostics data in toonear real-time insights on your Azure services.</span></span> <span data-ttu-id="b4043-109">[Bu belge makalesi nasıl tooset Event Hubs, Yukarı Akış Analizi ile verileri işlemek ve Powerbı çıkış olarak kullanmak iyi bir genel bakış sağlayan](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="b4043-109">[This documentation article gives a great overview of how tooset up Event Hubs, process data with Stream Analytics, and use PowerBI as an output](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span> <span data-ttu-id="b4043-110">Aşağıda, tanılama günlükleri ile ayarlanan için birkaç ipucu verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b4043-110">Here are a few tips for getting set up with diagnostic logs:</span></span>
  
  * <span data-ttu-id="b4043-111">Merhaba portal hello seçeneğinde denetlemek veya tooselect hello event hub'ında ile başlayan hello adlı ad alanı hello istediğiniz şekilde PowerShell aracılığıyla etkinleştirmek bir event hub'tanılama günlükleri kategorisi için otomatik olarak oluşturulan **ınsights**.</span><span class="sxs-lookup"><span data-stu-id="b4043-111">An event hub for a category of diagnostic logs is created automatically when you check hello option in hello portal or enable it through PowerShell, so you want tooselect hello event hub in hello namespace with hello name that starts with **insights-**.</span></span>
  * <span data-ttu-id="b4043-112">SQL koddan hello olan örnek Stream Analytics sorgu tooparse tooa Powerbı tablodaki tüm hello günlük verilerini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b4043-112">hello following SQL code is a sample Stream Analytics query that you can use tooparse all hello log data in tooa PowerBI table:</span></span>

    ```sql
    SELECT
    records.ArrayValue.[Properties you want tootrack]
    INTO
    [OutputSourceName – hello PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* <span data-ttu-id="b4043-113">**Bir özel telemetri ve günlüğe kaydetme platformu yapı** – özel olarak geliştirilmiş telemetri platform zaten varsa veya olan yalnızca bir hello yüksek düzeyde ölçeklenebilir yayımlama-abonelik oluşturma hakkında olay hub'ları yapısını tooflexibly verir düşünüyorum alma tanılama günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="b4043-113">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, hello highly scalable publish-subscribe nature of Event Hubs allows you tooflexibly ingest diagnostic logs.</span></span> <span data-ttu-id="b4043-114">[Bir küresel ölçekteki telemetri Platform dan Rosanova'nın Kılavuzu toousing olay hub'ları bkz](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span><span class="sxs-lookup"><span data-stu-id="b4043-114">[See Dan Rosanova’s guide toousing Event Hubs in a global scale telemetry platform here](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="enable-streaming-of-diagnostic-logs"></a><span data-ttu-id="b4043-115">Tanılama günlüklerini akışı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="b4043-115">Enable streaming of diagnostic logs</span></span>
<span data-ttu-id="b4043-116">Tanılama günlüklerini hello portalı yoluyla programlı olarak akış veya hello kullanarak etkinleştirebilirsiniz [Azure İzleyici REST API'lerini](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span><span class="sxs-lookup"><span data-stu-id="b4043-116">You can enable streaming of diagnostic logs programmatically, via hello portal, or using hello [Azure Monitor REST APIs](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span></span> <span data-ttu-id="b4043-117">Her iki durumda da, oluşturduğunuz bir tanılama ayarını belirttiğiniz bir olay hub'ları ad alanı ve hello günlük kategorileri ve toosend toohello ad alanında istediğiniz ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="b4043-117">Either way, you create a diagnostic setting in which you specify an Event Hubs namespace and hello log categories and metrics you want toosend in toohello namespace.</span></span> <span data-ttu-id="b4043-118">Bir olay hub'ı etkinleştirmeniz her günlük kategori için hello ad alanı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b4043-118">An event hub is created in hello namespace for each log category you enable.</span></span> <span data-ttu-id="b4043-119">Bir tanılama **günlük kategori** kaynak toplayabilir günlük türüdür.</span><span class="sxs-lookup"><span data-stu-id="b4043-119">A diagnostic **log category** is a type of log that a resource may collect.</span></span>

> [!WARNING]
> <span data-ttu-id="b4043-120">Etkinleştirme ve işlem kaynakları (örneğin, VM'ler veya Service Fabric) tanılama günlükleri akış [adımları farklı bir dizi gerektirir](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span><span class="sxs-lookup"><span data-stu-id="b4043-120">Enabling and streaming diagnostic logs from Compute resources (for example, VMs or Service Fabric) [requires a different set of steps](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span></span>
> 
> 

<span data-ttu-id="b4043-121">ad alanı toobe sahip olmayan Hello hizmet veri yolu veya olay hub'ları uygun RBAC erişim tooboth abonelikleri hello ayarı yapılandıran hello kullanıcının sahip olduğu sürece günlükleri yayma hello kaynak aynı abonelik hello.</span><span class="sxs-lookup"><span data-stu-id="b4043-121">hello Service Bus or Event Hubs namespace does not have toobe in hello same subscription as hello resource emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="stream-diagnostic-logs-using-hello-portal"></a><span data-ttu-id="b4043-122">Merhaba portalı kullanarak akış tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="b4043-122">Stream diagnostic logs using hello portal</span></span>
1. <span data-ttu-id="b4043-123">Merhaba portalında tooAzure İzleyici gidin ve tıklayın **tanılama ayarları**</span><span class="sxs-lookup"><span data-stu-id="b4043-123">In hello portal, navigate tooAzure Monitor and click on **Diagnostic Settings**</span></span>

    ![Azure İzleyicisi İzleme bölümü](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. <span data-ttu-id="b4043-125">İsteğe bağlı olarak kaynak grubu veya kaynak türü tarafından hello listesini filtrelemek ve tooset tanılama ayarını istediğiniz hello kaynakta'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b4043-125">Optionally filter hello list by resource group or resource type, then click on hello resource for which you would like tooset a diagnostic setting.</span></span>

3. <span data-ttu-id="b4043-126">Hiçbir ayar seçmiş olduğunuz hello kaynakta mevcut, istendiğinde toocreate bir ayar demektir.</span><span class="sxs-lookup"><span data-stu-id="b4043-126">If no settings exist on hello resource you have selected, you are prompted toocreate a setting.</span></span> <span data-ttu-id="b4043-127">"Tanılamayı açın."'i tıklatın</span><span class="sxs-lookup"><span data-stu-id="b4043-127">Click "Turn on diagnostics."</span></span>

   ![Tanılama ayarını - ayar Ekle](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   <span data-ttu-id="b4043-129">Merhaba kaynakta mevcut ayarları varsa, bu kaynak üzerinde zaten yapılandırılmış ayarları listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b4043-129">If there are existing settings on hello resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="b4043-130">"Tanılama ayarını Ekle" yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b4043-130">Click "Add diagnostic setting."</span></span>

   ![Tanılama ayarını ayarlar varolan - Ekle](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="b4043-132">Ayarı, bir ad verin ve hello kutuyu **tooan event hub'ı akış**, bir olay hub'ları ad alanı seçin.</span><span class="sxs-lookup"><span data-stu-id="b4043-132">Give your setting a name and check hello box for **Stream tooan event hub**, then select an Event Hubs namespace.</span></span>
   
   ![Tanılama ayarını ayarlar varolan - Ekle](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   <span data-ttu-id="b4043-134">Merhaba seçili ad alanı burada hello olay hub'ı (Bu akış tanılama günlükleri, ilk kez kullanıyorsanız) oluşturulur veya çok akışı olacaktır (olup olmadığını zaten o günlük kategori toothis ad akış kaynakları), ve hello İlkesi hello tanımlar Akış mekanizması hello izinlerine sahip değil.</span><span class="sxs-lookup"><span data-stu-id="b4043-134">hello namespace selected will be where hello event hub is created (if this is your first time streaming diagnostic logs) or streamed too(if there are already resources that are streaming that log category toothis namespace), and hello policy defines hello permissions that hello streaming mechanism has.</span></span> <span data-ttu-id="b4043-135">Bugün, tooan akış olay hub'ı yönetme, gönderme ve dinleme izinleri gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b4043-135">Today, streaming tooan event hub requires Manage, Send, and Listen permissions.</span></span> <span data-ttu-id="b4043-136">Oluşturun veya olay hub'ları ad alanı paylaşılan erişim ilkeleri hello portalında Merhaba yapılandırma sekmesi altında ad alanınız için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b4043-136">You can create or modify Event Hubs namespace shared access policies in hello portal under hello Configure tab for your namespace.</span></span> <span data-ttu-id="b4043-137">tooupdate Bu tanılama ayarlardan biri, hello istemci hello olay hub'ları yetkilendirme kuralı hello ListKey izninizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4043-137">tooupdate one of these diagnostic settings, hello client must have hello ListKey permission on hello Event Hubs authorization rule.</span></span>

4. <span data-ttu-id="b4043-138">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b4043-138">Click **Save**.</span></span>

<span data-ttu-id="b4043-139">Birkaç dakika sonra bu kaynak için ayarları listenizden hello yeni ayar görünür ve yeni olay verilerini oluşturulan hemen tanılama günlüklerini toothat depolama hesabı akışa alınır.</span><span class="sxs-lookup"><span data-stu-id="b4043-139">After a few moments, hello new setting appears in your list of settings for this resource, and diagnostic logs are streamed toothat storage account as soon as new event data is generated.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="b4043-140">PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="b4043-140">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="b4043-141">Merhaba akış tooenable [Azure PowerShell cmdlet'leri](insights-powershell-samples.md), hello kullanabilirsiniz `Set-AzureRmDiagnosticSetting` Bu parametreler cmdlet'iyle:</span><span class="sxs-lookup"><span data-stu-id="b4043-141">tooenable streaming via hello [Azure PowerShell Cmdlets](insights-powershell-samples.md), you can use hello `Set-AzureRmDiagnosticSetting` cmdlet with these parameters:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

<span data-ttu-id="b4043-142">Merhaba Service Bus kural kimliği olduğundan bu biçiminde bir dize: `{Service Bus resource ID}/authorizationrules/{key name}`, örneğin, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span><span class="sxs-lookup"><span data-stu-id="b4043-142">hello Service Bus Rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`, for example, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span></span>

### <a name="via-azure-cli"></a><span data-ttu-id="b4043-143">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b4043-143">Via Azure CLI</span></span>
<span data-ttu-id="b4043-144">Merhaba akış tooenable [Azure CLI](insights-cli-samples.md), hello kullanabilirsiniz `insights diagnostic set` komut şöyle:</span><span class="sxs-lookup"><span data-stu-id="b4043-144">tooenable streaming via hello [Azure CLI](insights-cli-samples.md), you can use hello `insights diagnostic set` command like this:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

<span data-ttu-id="b4043-145">Aynı hizmet veri yolu kural kimliği için PowerShell Cmdlet hello için açıklandığı gibi biçimi hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="b4043-145">Use hello same format for Service Bus Rule ID as explained for hello PowerShell Cmdlet.</span></span>

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a><span data-ttu-id="b4043-146">Olay hub'ları hello günlük verilerini nasıl kullanabilir?</span><span class="sxs-lookup"><span data-stu-id="b4043-146">How do I consume hello log data from Event Hubs?</span></span>
<span data-ttu-id="b4043-147">Olay hub'ları örnek çıktı verilerini şöyledir:</span><span class="sxs-lookup"><span data-stu-id="b4043-147">Here is sample output data from Event Hubs:</span></span>

```json
{
    "records": [
        {
            "time": "2016-07-15T18:00:22.6235064Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330013509921957/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Error",
            "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T17:58:55.048482Z",
                "endTime": "2016-07-15T18:00:22.4109204Z",
                "status": "Failed",
                "code": "BadGateway",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330013509921957",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "29a9862f-969b-4c70-90c4-dfbdc814e413",
                    "clientTrackingId": "08587330013509921958"
                }
            }
        },
        {
            "time": "2016-07-15T18:01:15.7532989Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330012106702630/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Information",
            "operationName": "Microsoft.Logic/workflows/workflowActionStarted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T18:01:15.5828115Z",
                "status": "Running",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330012106702630",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "042fb72c-7bd4-439e-89eb-3cf4409d429e",
                    "clientTrackingId": "08587330012106702632"
                }
            }
        }
    ]
}
```

| <span data-ttu-id="b4043-148">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="b4043-148">Element Name</span></span> | <span data-ttu-id="b4043-149">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b4043-149">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b4043-150">kayıtları</span><span class="sxs-lookup"><span data-stu-id="b4043-150">records</span></span> |<span data-ttu-id="b4043-151">Bu yük tüm günlük olaylar dizisi.</span><span class="sxs-lookup"><span data-stu-id="b4043-151">An array of all log events in this payload.</span></span> |
| <span data-ttu-id="b4043-152">time</span><span class="sxs-lookup"><span data-stu-id="b4043-152">time</span></span> |<span data-ttu-id="b4043-153">Merhaba olay gerçekleştiği zaman.</span><span class="sxs-lookup"><span data-stu-id="b4043-153">Time at which hello event occurred.</span></span> |
| <span data-ttu-id="b4043-154">category</span><span class="sxs-lookup"><span data-stu-id="b4043-154">category</span></span> |<span data-ttu-id="b4043-155">Bu olay günlüğü kategori.</span><span class="sxs-lookup"><span data-stu-id="b4043-155">Log category for this event.</span></span> |
| <span data-ttu-id="b4043-156">resourceId</span><span class="sxs-lookup"><span data-stu-id="b4043-156">resourceId</span></span> |<span data-ttu-id="b4043-157">Bu olayı oluşturan hello kaynağının kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="b4043-157">Resource ID of hello resource that generated this event.</span></span> |
| <span data-ttu-id="b4043-158">operationName</span><span class="sxs-lookup"><span data-stu-id="b4043-158">operationName</span></span> |<span data-ttu-id="b4043-159">Merhaba işlemin adı.</span><span class="sxs-lookup"><span data-stu-id="b4043-159">Name of hello operation.</span></span> |
| <span data-ttu-id="b4043-160">düzeyi</span><span class="sxs-lookup"><span data-stu-id="b4043-160">level</span></span> |<span data-ttu-id="b4043-161">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="b4043-161">Optional.</span></span> <span data-ttu-id="b4043-162">Merhaba günlük olay düzeyini gösterir.</span><span class="sxs-lookup"><span data-stu-id="b4043-162">Indicates hello log event level.</span></span> |
| <span data-ttu-id="b4043-163">properties</span><span class="sxs-lookup"><span data-stu-id="b4043-163">properties</span></span> |<span data-ttu-id="b4043-164">Merhaba olay özellikleri.</span><span class="sxs-lookup"><span data-stu-id="b4043-164">Properties of hello event.</span></span> |

<span data-ttu-id="b4043-165">TooEvent hub akış destekleyen tüm kaynak sağlayıcılarının bir listesini görüntüleyebileceğiniz [burada](monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="b4043-165">You can view a list of all resource providers that support streaming tooEvent Hubs [here](monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="stream-data-from-compute-resources"></a><span data-ttu-id="b4043-166">İşlem kaynaklardan veri akışı</span><span class="sxs-lookup"><span data-stu-id="b4043-166">Stream data from Compute resources</span></span>
<span data-ttu-id="b4043-167">Ayrıca hello Windows Azure Tanılama aracı kullanarak işlem kaynaklarını tanılama günlükleri akışını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4043-167">You can also stream diagnostic logs from Compute resources using hello Windows Azure Diagnostics agent.</span></span> <span data-ttu-id="b4043-168">[Bu makaleye bakın](../event-hubs/event-hubs-streaming-azure-diags-data.md) nasıl tooset o yukarı.</span><span class="sxs-lookup"><span data-stu-id="b4043-168">[See this article](../event-hubs/event-hubs-streaming-azure-diags-data.md) for how tooset that up.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4043-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b4043-169">Next steps</span></span>
* [<span data-ttu-id="b4043-170">Azure tanılama günlükleri hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="b4043-170">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="b4043-171">Event Hubs kullanmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="b4043-171">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

