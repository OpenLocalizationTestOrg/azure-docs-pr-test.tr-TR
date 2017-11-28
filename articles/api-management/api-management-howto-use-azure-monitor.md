---
title: "aaaMonitor Azure İzleyicisi ile API Management | Microsoft Docs"
description: "Nasıl toomonitor Azure API Management hizmet Azure İzleyicisi'ni kullanma hakkında bilgi edinin."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 5012d8ed57ea4f94ea6bc1b7c4e1102516ec4414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a><span data-ttu-id="3853c-103">Azure İzleyicisi ile İzleyici API Yönetimi</span><span class="sxs-lookup"><span data-stu-id="3853c-103">Monitor API Management with Azure Monitor</span></span>
<span data-ttu-id="3853c-104">Azure İzleyicisi tüm Azure kaynakları izlemek için tek bir kaynak sağlayan bir Azure hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="3853c-104">Azure Monitor is an Azure service that provides a single source for monitoring all your Azure resources.</span></span> <span data-ttu-id="3853c-105">Azure izleme ile görselleştirme, sorgulama yapabilir, yönlendirmek, arşiv ve hello ölçümleri ve API Management gibi Azure kaynakları'ten gelen günlükleri eylemleri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="3853c-105">With Azure Monitor, you can visualize, query, route, archive, and take actions on hello metrics and logs coming from Azure resources such as API Management.</span></span> 

<span data-ttu-id="3853c-106">Video gösterileri nasıl aşağıdaki hello toomonitor API Azure İzleyicisi'ni kullanarak yönetim.</span><span class="sxs-lookup"><span data-stu-id="3853c-106">hello following video shows how toomonitor API Management using Azure Monitor.</span></span> <span data-ttu-id="3853c-107">Azure İzleyicisi hakkında daha fazla bilgi için bkz: [Azure İzleyicisi ile çalışmaya başlama].</span><span class="sxs-lookup"><span data-stu-id="3853c-107">For more information about Azure Monitor, see [Get Started with Azure Monitor].</span></span> 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a><span data-ttu-id="3853c-108">Ölçümler</span><span class="sxs-lookup"><span data-stu-id="3853c-108">Metrics</span></span>
<span data-ttu-id="3853c-109">API Management anda beş ölçümleri yayar ve biz tooadd hello gelecekte daha fazla planlayın.</span><span class="sxs-lookup"><span data-stu-id="3853c-109">API Management currently emits five metrics and we plan tooadd more in hello future.</span></span> <span data-ttu-id="3853c-110">Bu ölçümleri her dakika hello durumu ve Apı'lerinizi durumunu gerçek zamanlı görünürlük yakın vermiş gösterilen.</span><span class="sxs-lookup"><span data-stu-id="3853c-110">These metrics are emitted every minute, giving you near real-time visibility into hello state and health of your APIs.</span></span> <span data-ttu-id="3853c-111">Merhaba ölçümleri bir özeti aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="3853c-111">Following is a summary of hello metrics:</span></span>
* <span data-ttu-id="3853c-112">: Toplam ağ geçidi API hello sayısı hello dönemde istekleri.</span><span class="sxs-lookup"><span data-stu-id="3853c-112">Total Gateway Requests: hello number of API requests in hello period.</span></span> 
* <span data-ttu-id="3853c-113">Başarılı ağ geçidi istekleri: 304, 307 ve 301 (örneğin, 200) daha küçük bir şey de dahil olmak üzere başarılı HTTP yanıt kodları alınan API istek hello sayısı.</span><span class="sxs-lookup"><span data-stu-id="3853c-113">Successful Gateway Requests: hello number of API requests that received successful HTTP response codes including 304, 307 and anything smaller than 301 (for example, 200).</span></span> 
* <span data-ttu-id="3853c-114">Ağ geçidi isteği başarısız oldu: hello hatalı HTTP yanıt kodu 400 ve 500'den büyük herhangi bir şey de dahil olmak üzere alınan API istek sayısı.</span><span class="sxs-lookup"><span data-stu-id="3853c-114">Failed Gateway Requests: hello number of API requests that received erroneous HTTP response codes including 400 and anything larger than 500.</span></span>
* <span data-ttu-id="3853c-115">Yetkisiz ağ geçidi istekleri: HTTP yanıt kodları 401, 403 ve 429 dahil alınan API istek hello sayısı.</span><span class="sxs-lookup"><span data-stu-id="3853c-115">Unauthorized Gateway Requests: hello number of API requests that received HTTP response codes including 401, 403, and 429.</span></span> 
* <span data-ttu-id="3853c-116">Diğer ağ geçidi istekleri: Kategoriler (örneğin, 418) önceki hello tooany ait değil HTTP yanıt kodları alınan API istek hello sayısı.</span><span class="sxs-lookup"><span data-stu-id="3853c-116">Other Gateway Requests: hello number of API requests that received HTTP response codes that do not belong tooany of hello preceding categories (for example, 418).</span></span>

<span data-ttu-id="3853c-117">API Management hizmetiniz ölçümlerini ya da Azure İzleyicisi'nde tüm Azure kaynaklarına erişim ölçümlerini erişebilir.</span><span class="sxs-lookup"><span data-stu-id="3853c-117">You can access metrics in your API Management service, or access metrics of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="3853c-118">API Management hizmetiniz tooview ölçümlerini:</span><span class="sxs-lookup"><span data-stu-id="3853c-118">tooview metrics in your API Management service:</span></span>
1. <span data-ttu-id="3853c-119">Açık hello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="3853c-119">Open hello Azure portal.</span></span>
2. <span data-ttu-id="3853c-120">Tooyour API Management hizmeti gidin.</span><span class="sxs-lookup"><span data-stu-id="3853c-120">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="3853c-121">Tıklatın **ölçümleri**.</span><span class="sxs-lookup"><span data-stu-id="3853c-121">Click **Metrics**.</span></span>

![Ölçüm dikey penceresi][metrics-blade]

<span data-ttu-id="3853c-123">Hakkında daha fazla bilgi için toouse ölçümler görmek [genel bakış, ölçümleri].</span><span class="sxs-lookup"><span data-stu-id="3853c-123">For more information about how toouse Metrics, see [Overview of Metrics].</span></span>

## <a name="activity-logs"></a><span data-ttu-id="3853c-124">Etkinlik Günlükleri</span><span class="sxs-lookup"><span data-stu-id="3853c-124">Activity Logs</span></span>
<span data-ttu-id="3853c-125">Etkinlik günlükleri, API Management services üzerinde gerçekleştirilen hello işlemlerinin bir anlayış sağlar.</span><span class="sxs-lookup"><span data-stu-id="3853c-125">Activity logs provide insight into hello operations that were performed on your API Management services.</span></span> <span data-ttu-id="3853c-126">Daha önce "denetim günlüklerini" veya "işletimsel logs" olarak bilinirdi.</span><span class="sxs-lookup"><span data-stu-id="3853c-126">It was previously known as "audit logs" or "operational logs".</span></span> <span data-ttu-id="3853c-127">Etkinlik Günlükleri'ni kullanarak hello belirleyebilirsiniz "ne, kimin, ne zaman ve" herhangi bir yazma, API Management hizmetlerde yapılan işlemleri (PUT, POST, DELETE) için.</span><span class="sxs-lookup"><span data-stu-id="3853c-127">Using activity logs, you can determine hello "what, who, and when" for any write operations (PUT, POST, DELETE) taken on your API Management services.</span></span> 

> [!NOTE]
> <span data-ttu-id="3853c-128">Etkinlik günlükleri okuma (GET) işlemleri veya başlığında gerçekleştirilen işlemleri dahil değil Klasik yayımcı portalı hello veya hello özgün yönetim API'leri kullanılarak.</span><span class="sxs-lookup"><span data-stu-id="3853c-128">Activity logs do not include read (GET) operations or operations performed in hello classic Publisher Portal or using hello original Management APIs.</span></span>

<span data-ttu-id="3853c-129">API Management hizmetiniz etkinlik günlükleri erişmek veya günlükleri, Azure kaynaklarınızın Azure İzleyicisi'nde erişim.</span><span class="sxs-lookup"><span data-stu-id="3853c-129">You can access activity logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="3853c-130">API Management hizmetiniz tooview etkinliğini kaydeder:</span><span class="sxs-lookup"><span data-stu-id="3853c-130">tooview activity logs in your API Management service:</span></span>
1. <span data-ttu-id="3853c-131">Açık hello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="3853c-131">Open hello Azure portal.</span></span>
2. <span data-ttu-id="3853c-132">Tooyour API Management hizmeti gidin.</span><span class="sxs-lookup"><span data-stu-id="3853c-132">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="3853c-133">Tıklatın **etkinlik günlüğü**.</span><span class="sxs-lookup"><span data-stu-id="3853c-133">Click **Activity log**.</span></span>

![Etkinlik günlükleri dikey penceresi][activity-logs-blade]

<span data-ttu-id="3853c-135">Hakkında daha fazla bilgi için toouse ölçümler görmek [etkinlik günlükleri genel bakış].</span><span class="sxs-lookup"><span data-stu-id="3853c-135">For more information about how toouse Metrics, see [Overview of Activity Logs].</span></span>

## <a name="alerts"></a><span data-ttu-id="3853c-136">Uyarılar</span><span class="sxs-lookup"><span data-stu-id="3853c-136">Alerts</span></span>
<span data-ttu-id="3853c-137">Ölçümleri ve etkinlik açtığında temelinde tooreceive uyarılar yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3853c-137">You can configure tooreceive alerts based on metrics and activity logs.</span></span> <span data-ttu-id="3853c-138">Azure İzleyici tetikler olduğunda bir uyarı toodo hello aşağıdaki tooconfigure sağlar:</span><span class="sxs-lookup"><span data-stu-id="3853c-138">Azure Monitor allows you tooconfigure an alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="3853c-139">Bir e-posta bildirimi gönder</span><span class="sxs-lookup"><span data-stu-id="3853c-139">Send an email notification</span></span>
* <span data-ttu-id="3853c-140">bir Web kancası çağırın</span><span class="sxs-lookup"><span data-stu-id="3853c-140">Call a webhook</span></span>
* <span data-ttu-id="3853c-141">Bir Azure mantıksal uygulamayı çağırmak</span><span class="sxs-lookup"><span data-stu-id="3853c-141">Invoke an Azure Logic App</span></span>

<span data-ttu-id="3853c-142">API Management hizmetiniz veya Azure İzleyicisi uyarı kuralları yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3853c-142">You can configure alert rules in your API Management service, or in Azure Monitor.</span></span> <span data-ttu-id="3853c-143">tooconfigure API Management bunları:</span><span class="sxs-lookup"><span data-stu-id="3853c-143">tooconfigure them in API Management:</span></span> 
1. <span data-ttu-id="3853c-144">Açık hello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="3853c-144">Open hello Azure portal.</span></span>
2. <span data-ttu-id="3853c-145">Tooyour API Management hizmeti gidin.</span><span class="sxs-lookup"><span data-stu-id="3853c-145">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="3853c-146">Tıklatın **uyarı kuralları**.</span><span class="sxs-lookup"><span data-stu-id="3853c-146">Click **Alert rules**.</span></span>

![Uyarı kuralları dikey penceresi][alert-rules-blade]

<span data-ttu-id="3853c-148">Uyarıları kullanma hakkında daha fazla bilgi için bkz: [genel bakış, uyarıları].</span><span class="sxs-lookup"><span data-stu-id="3853c-148">For more information about using Alerts, see [Overview of Alerts].</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="3853c-149">Tanılama Günlükleri</span><span class="sxs-lookup"><span data-stu-id="3853c-149">Diagnostic Logs</span></span>
<span data-ttu-id="3853c-150">Tanılama günlüklerini işlemleri ve denetim yanı sıra sorun giderme amacıyla önemli hataları hakkında zengin bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="3853c-150">Diagnostic logs provide rich information about operations and errors that are important for auditing as well as troubleshooting purposes.</span></span> <span data-ttu-id="3853c-151">Tanılama günlükleri, etkinlik günlükleri farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="3853c-151">Diagnostics logs differ from activity logs.</span></span> <span data-ttu-id="3853c-152">Etkinlik günlükleri Azure kaynaklarınızı üzerinde gerçekleştirilen hello işlemlerinin fikir sağlar.</span><span class="sxs-lookup"><span data-stu-id="3853c-152">Activity logs provide insights into hello operations that were performed on your Azure resources.</span></span> <span data-ttu-id="3853c-153">Tanılama günlükleri işlemleri kaynağınız kendisini gerçekleştirilen bir anlayış sağlar.</span><span class="sxs-lookup"><span data-stu-id="3853c-153">Diagnostics logs provide insight into operations that your resource performed itself.</span></span>

<span data-ttu-id="3853c-154">API Management anda tanılama sağlar (saatlik toplu hale) günlükleri ayrı API'si hakkında isteği yapı izlenerek hello sahip her girişi:</span><span class="sxs-lookup"><span data-stu-id="3853c-154">API Management currently provides diagnostics logs (batched hourly) about individual API request with each entry having hello following structure:</span></span>

```
{
    "Tenant": "",
      "DeploymentName": "",
      "time": "",
      "resourceId": "",
      "category": "GatewayLogs",
      "operationName": "Microsoft.ApiManagement/GatewayLogs",
      "durationMs": ,
      "Level": ,
      "properties": "{
          "ApiId": "",
          "OperationId": "",
          "ProductId": "",
          "SubscriptionId": "",
          "Method": "",
          "Url": "",
          "RequestSize": ,
          "ServiceTime": "",
          "BackendMethod": "",
          "BackendUrl": "",
          "BackendResponseCode": ,
          "ResponseCode": ,
          "ResponseSize": ,
          "Cache": "",
          "UserId"
      }"
 }
```

<span data-ttu-id="3853c-155">API Management hizmetiniz tanılama günlüklerine erişmek veya günlükleri, Azure kaynaklarınızın Azure İzleyicisi'nde erişim.</span><span class="sxs-lookup"><span data-stu-id="3853c-155">You can access diagnostic logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="3853c-156">API Management hizmetiniz tanılama günlüklerine tooview:</span><span class="sxs-lookup"><span data-stu-id="3853c-156">tooview diagnostic logs in your API Management service:</span></span>
1. <span data-ttu-id="3853c-157">Açık hello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="3853c-157">Open hello Azure portal.</span></span>
2. <span data-ttu-id="3853c-158">Tooyour API Management hizmeti gidin.</span><span class="sxs-lookup"><span data-stu-id="3853c-158">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="3853c-159">Tıklatın **tanılama günlük**.</span><span class="sxs-lookup"><span data-stu-id="3853c-159">Click **Diagnostic log**.</span></span>

![Tanılama günlükleri dikey penceresi][diagnostic-logs-blade]

<span data-ttu-id="3853c-161">Hakkında daha fazla bilgi için toouse ölçümler görmek [tanılama günlükleri'ne genel bakış].</span><span class="sxs-lookup"><span data-stu-id="3853c-161">For more information about how toouse Metrics, see [Overview of Diagnostic Logs].</span></span>

## <a name="next-step"></a><span data-ttu-id="3853c-162">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="3853c-162">Next Step</span></span>

* <span data-ttu-id="3853c-163">[Azure İzleyicisi ile çalışmaya başlama]</span><span class="sxs-lookup"><span data-stu-id="3853c-163">[Get Started with Azure Monitor]</span></span>
* <span data-ttu-id="3853c-164">[genel bakış, ölçümleri]</span><span class="sxs-lookup"><span data-stu-id="3853c-164">[Overview of Metrics]</span></span>
* <span data-ttu-id="3853c-165">[etkinlik günlükleri genel bakış]</span><span class="sxs-lookup"><span data-stu-id="3853c-165">[Overview of Activity Logs]</span></span>
* <span data-ttu-id="3853c-166">[tanılama günlükleri'ne genel bakış]</span><span class="sxs-lookup"><span data-stu-id="3853c-166">[Overview of Diagnostic Logs]</span></span>
* <span data-ttu-id="3853c-167">[genel bakış, uyarıları]</span><span class="sxs-lookup"><span data-stu-id="3853c-167">[Overview of Alerts]</span></span>

[Azure İzleyicisi ile çalışmaya başlama]: ../monitoring-and-diagnostics/monitoring-get-started.md
[genel bakış, ölçümleri]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md
[etkinlik günlükleri genel bakış]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md
[tanılama günlükleri'ne genel bakış]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md
[genel bakış, uyarıları]: ../monitoring-and-diagnostics/insights-alerts-portal.md



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
