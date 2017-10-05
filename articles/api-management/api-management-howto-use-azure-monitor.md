---
title: "API Management ile Azure İzleyicisi İzleme | Microsoft Docs"
description: "Azure İzleyicisi'ni kullanarak Azure API Management hizmeti izleme öğrenin."
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
ms.openlocfilehash: 0f64947755c79739bb6f15325929bd074cfd7210
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a><span data-ttu-id="b616b-103">Azure İzleyicisi ile İzleyici API Yönetimi</span><span class="sxs-lookup"><span data-stu-id="b616b-103">Monitor API Management with Azure Monitor</span></span>
<span data-ttu-id="b616b-104">Azure İzleyicisi tüm Azure kaynakları izlemek için tek bir kaynak sağlayan bir Azure hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="b616b-104">Azure Monitor is an Azure service that provides a single source for monitoring all your Azure resources.</span></span> <span data-ttu-id="b616b-105">Azure izleme ile görselleştirme, sorgulama yapabilir, yönlendirmek, arşiv ve ölçümleri ve API Management gibi Azure kaynakları'ten gelen günlükleri eylemleri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="b616b-105">With Azure Monitor, you can visualize, query, route, archive, and take actions on the metrics and logs coming from Azure resources such as API Management.</span></span> 

<span data-ttu-id="b616b-106">Aşağıdaki video Azure İzleyicisi'ni kullanarak API Management izleme gösterir.</span><span class="sxs-lookup"><span data-stu-id="b616b-106">The following video shows how to monitor API Management using Azure Monitor.</span></span> <span data-ttu-id="b616b-107">Azure İzleyicisi hakkında daha fazla bilgi için bkz: [Azure İzleyicisi ile çalışmaya başlama].</span><span class="sxs-lookup"><span data-stu-id="b616b-107">For more information about Azure Monitor, see [Get Started with Azure Monitor].</span></span> 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a><span data-ttu-id="b616b-108">Ölçümler</span><span class="sxs-lookup"><span data-stu-id="b616b-108">Metrics</span></span>
<span data-ttu-id="b616b-109">API Management anda beş ölçümleri yayar ve gelecekte daha ekleme planlıyoruz.</span><span class="sxs-lookup"><span data-stu-id="b616b-109">API Management currently emits five metrics and we plan to add more in the future.</span></span> <span data-ttu-id="b616b-110">Bu ölçümler dakikada, Apı'lerinizi durumunu ve durumunu gerçek zamanlı görünürlük yakın vermiş gösterilen.</span><span class="sxs-lookup"><span data-stu-id="b616b-110">These metrics are emitted every minute, giving you near real-time visibility into the state and health of your APIs.</span></span> <span data-ttu-id="b616b-111">Ölçümler bir özeti aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b616b-111">Following is a summary of the metrics:</span></span>
* <span data-ttu-id="b616b-112">: Toplam ağ geçidi API sayısı dönemde istekleri.</span><span class="sxs-lookup"><span data-stu-id="b616b-112">Total Gateway Requests: the number of API requests in the period.</span></span> 
* <span data-ttu-id="b616b-113">Başarılı ağ geçidi istekleri: 304, 307 ve 301 (örneğin, 200) daha küçük bir şey de dahil olmak üzere başarılı HTTP yanıt kodları alınan API istek sayısı.</span><span class="sxs-lookup"><span data-stu-id="b616b-113">Successful Gateway Requests: the number of API requests that received successful HTTP response codes including 304, 307 and anything smaller than 301 (for example, 200).</span></span> 
* <span data-ttu-id="b616b-114">Başarısız olan ağ geçidi istekleri: Hatalı HTTP yanıt kodu 400 ve 500'den büyük herhangi bir şey de dahil olmak üzere alınan API istek sayısı.</span><span class="sxs-lookup"><span data-stu-id="b616b-114">Failed Gateway Requests: the number of API requests that received erroneous HTTP response codes including 400 and anything larger than 500.</span></span>
* <span data-ttu-id="b616b-115">Yetkisiz ağ geçidi istekleri: 401, 403 ve 429 dahil olmak üzere HTTP yanıt kodları alınan API istek sayısı.</span><span class="sxs-lookup"><span data-stu-id="b616b-115">Unauthorized Gateway Requests: the number of API requests that received HTTP response codes including 401, 403, and 429.</span></span> 
* <span data-ttu-id="b616b-116">Diğer ağ geçidi istekleri: önceki kategorileri (örneğin, 418) birine ait değil HTTP yanıt kodları alınan API istek sayısı.</span><span class="sxs-lookup"><span data-stu-id="b616b-116">Other Gateway Requests: the number of API requests that received HTTP response codes that do not belong to any of the preceding categories (for example, 418).</span></span>

<span data-ttu-id="b616b-117">API Management hizmetiniz ölçümlerini ya da Azure İzleyicisi'nde tüm Azure kaynaklarına erişim ölçümlerini erişebilir.</span><span class="sxs-lookup"><span data-stu-id="b616b-117">You can access metrics in your API Management service, or access metrics of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="b616b-118">API Management hizmetiniz ölçümleri görüntülemek için:</span><span class="sxs-lookup"><span data-stu-id="b616b-118">To view metrics in your API Management service:</span></span>
1. <span data-ttu-id="b616b-119">Azure Portalı'nı açın.</span><span class="sxs-lookup"><span data-stu-id="b616b-119">Open the Azure portal.</span></span>
2. <span data-ttu-id="b616b-120">API Management hizmetiniz gidin.</span><span class="sxs-lookup"><span data-stu-id="b616b-120">Go to your API Management service.</span></span>
3. <span data-ttu-id="b616b-121">Tıklatın **ölçümleri**.</span><span class="sxs-lookup"><span data-stu-id="b616b-121">Click **Metrics**.</span></span>

![Ölçüm dikey penceresi][metrics-blade]

<span data-ttu-id="b616b-123">Ölçümleri kullanma hakkında daha fazla bilgi için bkz: [genel bakış, ölçümleri].</span><span class="sxs-lookup"><span data-stu-id="b616b-123">For more information about how to use Metrics, see [Overview of Metrics].</span></span>

## <a name="activity-logs"></a><span data-ttu-id="b616b-124">Etkinlik Günlükleri</span><span class="sxs-lookup"><span data-stu-id="b616b-124">Activity Logs</span></span>
<span data-ttu-id="b616b-125">Etkinlik günlükleri, API Management services üzerinde gerçekleştirilen işlemler hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b616b-125">Activity logs provide insight into the operations that were performed on your API Management services.</span></span> <span data-ttu-id="b616b-126">Daha önce "denetim günlüklerini" veya "işletimsel logs" olarak bilinirdi.</span><span class="sxs-lookup"><span data-stu-id="b616b-126">It was previously known as "audit logs" or "operational logs".</span></span> <span data-ttu-id="b616b-127">Etkinlik Günlükleri'ni kullanarak, belirleyebilirsiniz "ne, kimin, ne zaman ve" herhangi bir yazma, API Management hizmetlerde yapılan işlemleri (PUT, POST, DELETE) için.</span><span class="sxs-lookup"><span data-stu-id="b616b-127">Using activity logs, you can determine the "what, who, and when" for any write operations (PUT, POST, DELETE) taken on your API Management services.</span></span> 

> [!NOTE]
> <span data-ttu-id="b616b-128">Etkinlik günlükleri okuma (GET) işlemleri veya Klasik yayımcı portalında gerçekleştirilen veya özgün yönetim API'leri kullanılarak işlemleri içermez.</span><span class="sxs-lookup"><span data-stu-id="b616b-128">Activity logs do not include read (GET) operations or operations performed in the classic Publisher Portal or using the original Management APIs.</span></span>

<span data-ttu-id="b616b-129">API Management hizmetiniz etkinlik günlükleri erişmek veya günlükleri, Azure kaynaklarınızın Azure İzleyicisi'nde erişim.</span><span class="sxs-lookup"><span data-stu-id="b616b-129">You can access activity logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="b616b-130">Etkinliğini görüntülemek için API Management hizmetiniz kaydeder:</span><span class="sxs-lookup"><span data-stu-id="b616b-130">To view activity logs in your API Management service:</span></span>
1. <span data-ttu-id="b616b-131">Azure Portalı'nı açın.</span><span class="sxs-lookup"><span data-stu-id="b616b-131">Open the Azure portal.</span></span>
2. <span data-ttu-id="b616b-132">API Management hizmetiniz gidin.</span><span class="sxs-lookup"><span data-stu-id="b616b-132">Go to your API Management service.</span></span>
3. <span data-ttu-id="b616b-133">Tıklatın **etkinlik günlüğü**.</span><span class="sxs-lookup"><span data-stu-id="b616b-133">Click **Activity log**.</span></span>

![Etkinlik günlükleri dikey penceresi][activity-logs-blade]

<span data-ttu-id="b616b-135">Ölçümleri kullanma hakkında daha fazla bilgi için bkz: [etkinlik günlükleri genel bakış].</span><span class="sxs-lookup"><span data-stu-id="b616b-135">For more information about how to use Metrics, see [Overview of Activity Logs].</span></span>

## <a name="alerts"></a><span data-ttu-id="b616b-136">Uyarılar</span><span class="sxs-lookup"><span data-stu-id="b616b-136">Alerts</span></span>
<span data-ttu-id="b616b-137">Ölçümleri ve etkinlik açtığında göre uyarıları almak üzere yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b616b-137">You can configure to receive alerts based on metrics and activity logs.</span></span> <span data-ttu-id="b616b-138">Azure İzleyici tetikler, aşağıdakileri yapmak için bir uyarı yapılandırmanıza olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="b616b-138">Azure Monitor allows you to configure an alert to do the following when it triggers:</span></span>

* <span data-ttu-id="b616b-139">Bir e-posta bildirimi gönder</span><span class="sxs-lookup"><span data-stu-id="b616b-139">Send an email notification</span></span>
* <span data-ttu-id="b616b-140">bir Web kancası çağırın</span><span class="sxs-lookup"><span data-stu-id="b616b-140">Call a webhook</span></span>
* <span data-ttu-id="b616b-141">Bir Azure mantıksal uygulamayı çağırmak</span><span class="sxs-lookup"><span data-stu-id="b616b-141">Invoke an Azure Logic App</span></span>

<span data-ttu-id="b616b-142">API Management hizmetiniz veya Azure İzleyicisi uyarı kuralları yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b616b-142">You can configure alert rules in your API Management service, or in Azure Monitor.</span></span> <span data-ttu-id="b616b-143">API Management'te yapılandırmak için:</span><span class="sxs-lookup"><span data-stu-id="b616b-143">To configure them in API Management:</span></span> 
1. <span data-ttu-id="b616b-144">Azure Portalı'nı açın.</span><span class="sxs-lookup"><span data-stu-id="b616b-144">Open the Azure portal.</span></span>
2. <span data-ttu-id="b616b-145">API Management hizmetiniz gidin.</span><span class="sxs-lookup"><span data-stu-id="b616b-145">Go to your API Management service.</span></span>
3. <span data-ttu-id="b616b-146">Tıklatın **uyarı kuralları**.</span><span class="sxs-lookup"><span data-stu-id="b616b-146">Click **Alert rules**.</span></span>

![Uyarı kuralları dikey penceresi][alert-rules-blade]

<span data-ttu-id="b616b-148">Uyarıları kullanma hakkında daha fazla bilgi için bkz: [genel bakış, uyarıları].</span><span class="sxs-lookup"><span data-stu-id="b616b-148">For more information about using Alerts, see [Overview of Alerts].</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="b616b-149">Tanılama Günlükleri</span><span class="sxs-lookup"><span data-stu-id="b616b-149">Diagnostic Logs</span></span>
<span data-ttu-id="b616b-150">Tanılama günlüklerini işlemleri ve denetim yanı sıra sorun giderme amacıyla önemli hataları hakkında zengin bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b616b-150">Diagnostic logs provide rich information about operations and errors that are important for auditing as well as troubleshooting purposes.</span></span> <span data-ttu-id="b616b-151">Tanılama günlükleri, etkinlik günlükleri farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="b616b-151">Diagnostics logs differ from activity logs.</span></span> <span data-ttu-id="b616b-152">Etkinlik günlükleri Azure kaynaklarınızı üzerinde gerçekleştirilen işlemler fikir sağlar.</span><span class="sxs-lookup"><span data-stu-id="b616b-152">Activity logs provide insights into the operations that were performed on your Azure resources.</span></span> <span data-ttu-id="b616b-153">Tanılama günlükleri işlemleri kaynağınız kendisini gerçekleştirilen bir anlayış sağlar.</span><span class="sxs-lookup"><span data-stu-id="b616b-153">Diagnostics logs provide insight into operations that your resource performed itself.</span></span>

<span data-ttu-id="b616b-154">API Management anda tanılama sağlar (saatlik toplu hale) günlükleri ayrı API'si hakkında aşağıdaki yapıya sahip her girişi iste:</span><span class="sxs-lookup"><span data-stu-id="b616b-154">API Management currently provides diagnostics logs (batched hourly) about individual API request with each entry having the following structure:</span></span>

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

<span data-ttu-id="b616b-155">API Management hizmetiniz tanılama günlüklerine erişmek veya günlükleri, Azure kaynaklarınızın Azure İzleyicisi'nde erişim.</span><span class="sxs-lookup"><span data-stu-id="b616b-155">You can access diagnostic logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="b616b-156">API Management hizmetiniz tanılama günlükleri görüntülemek için:</span><span class="sxs-lookup"><span data-stu-id="b616b-156">To view diagnostic logs in your API Management service:</span></span>
1. <span data-ttu-id="b616b-157">Azure Portalı'nı açın.</span><span class="sxs-lookup"><span data-stu-id="b616b-157">Open the Azure portal.</span></span>
2. <span data-ttu-id="b616b-158">API Management hizmetiniz gidin.</span><span class="sxs-lookup"><span data-stu-id="b616b-158">Go to your API Management service.</span></span>
3. <span data-ttu-id="b616b-159">Tıklatın **tanılama günlük**.</span><span class="sxs-lookup"><span data-stu-id="b616b-159">Click **Diagnostic log**.</span></span>

![Tanılama günlükleri dikey penceresi][diagnostic-logs-blade]

<span data-ttu-id="b616b-161">Ölçümleri kullanma hakkında daha fazla bilgi için bkz: [tanılama günlükleri'ne genel bakış].</span><span class="sxs-lookup"><span data-stu-id="b616b-161">For more information about how to use Metrics, see [Overview of Diagnostic Logs].</span></span>

## <a name="next-step"></a><span data-ttu-id="b616b-162">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="b616b-162">Next Step</span></span>

* <span data-ttu-id="b616b-163">[Azure İzleyicisi ile çalışmaya başlama]</span><span class="sxs-lookup"><span data-stu-id="b616b-163">[Get Started with Azure Monitor]</span></span>
* <span data-ttu-id="b616b-164">[genel bakış, ölçümleri]</span><span class="sxs-lookup"><span data-stu-id="b616b-164">[Overview of Metrics]</span></span>
* <span data-ttu-id="b616b-165">[etkinlik günlükleri genel bakış]</span><span class="sxs-lookup"><span data-stu-id="b616b-165">[Overview of Activity Logs]</span></span>
* <span data-ttu-id="b616b-166">[tanılama günlükleri'ne genel bakış]</span><span class="sxs-lookup"><span data-stu-id="b616b-166">[Overview of Diagnostic Logs]</span></span>
* <span data-ttu-id="b616b-167">[genel bakış, uyarıları]</span><span class="sxs-lookup"><span data-stu-id="b616b-167">[Overview of Alerts]</span></span>

<span data-ttu-id="b616b-168">[Azure İzleyicisi ile çalışmaya başlama]: ../monitoring-and-diagnostics/monitoring-get-started.md</span><span class="sxs-lookup"><span data-stu-id="b616b-168">[Get Started with Azure Monitor]: ../monitoring-and-diagnostics/monitoring-get-started.md</span></span>
<span data-ttu-id="b616b-169">[genel bakış, ölçümleri]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md</span><span class="sxs-lookup"><span data-stu-id="b616b-169">[Overview of Metrics]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md</span></span>
<span data-ttu-id="b616b-170">[etkinlik günlükleri genel bakış]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md</span><span class="sxs-lookup"><span data-stu-id="b616b-170">[Overview of Activity Logs]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md</span></span>
<span data-ttu-id="b616b-171">[tanılama günlükleri'ne genel bakış]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md</span><span class="sxs-lookup"><span data-stu-id="b616b-171">[Overview of Diagnostic Logs]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md</span></span>
<span data-ttu-id="b616b-172">[genel bakış, uyarıları]: ../monitoring-and-diagnostics/insights-alerts-portal.md</span><span class="sxs-lookup"><span data-stu-id="b616b-172">[Overview of Alerts]: ../monitoring-and-diagnostics/insights-alerts-portal.md</span></span>



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
