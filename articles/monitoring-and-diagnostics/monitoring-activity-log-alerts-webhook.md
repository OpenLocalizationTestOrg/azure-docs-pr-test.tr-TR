---
title: "Etkinlik günlüğü uyarıları kullanılan Web kancası şema anlama | Microsoft Docs"
description: "Bir etkinlik günlüğü uyarı etkinleştirdiğinde, bir Web kancası URL'si gönderilen JSON şeması hakkında bilgi edinin."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: 75c71bcd16573d4f4dd3377c623aa9b414aa3906
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a><span data-ttu-id="68579-103">Azure etkinlik günlüğü uyarılar için Web kancaları</span><span class="sxs-lookup"><span data-stu-id="68579-103">Webhooks for Azure activity log alerts</span></span>
<span data-ttu-id="68579-104">Bir eylem grubu tanımının bir parçası olarak, etkinlik günlüğü uyarı bildirimlerini almak için Web kancası uç noktalarını yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68579-104">As part of the definition of an action group, you can configure webhook endpoints to receive activity log alert notifications.</span></span> <span data-ttu-id="68579-105">Web kancası ile işlem sonrası ya da özel eylemler için diğer sistemlere bu bildirimler yönlendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68579-105">With webhooks, you can route these notifications to other systems for post-processing or custom actions.</span></span> <span data-ttu-id="68579-106">Bu makalede, bir Web kancası için HTTP POST için yükü nasıl göründüğünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="68579-106">This article shows what the payload for the HTTP POST to a webhook looks like.</span></span>

<span data-ttu-id="68579-107">Etkinlik günlüğü uyarılar hakkında daha fazla bilgi için bkz: nasıl yapılır [Azure etkinlik günlüğü uyarı oluşturma](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="68579-107">For more information on activity log alerts, see how to [create Azure activity log alerts](monitoring-activity-log-alerts.md).</span></span>

<span data-ttu-id="68579-108">Eylem grupları hakkında daha fazla bilgi için bkz: nasıl yapılır [Eylem grupları oluşturma](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="68579-108">For information on action groups, see how to [create action groups](monitoring-action-groups.md).</span></span>

## <a name="authenticate-the-webhook"></a><span data-ttu-id="68579-109">Web kancası kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="68579-109">Authenticate the webhook</span></span>
<span data-ttu-id="68579-110">Web kancası kimlik doğrulaması için isteğe bağlı olarak belirteç tabanlı bir yetkilendirme kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68579-110">The webhook can optionally use token-based authorization for authentication.</span></span> <span data-ttu-id="68579-111">URI kaydedilir belirteci Kimliğine sahip, örneğin, Web kancası `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span><span class="sxs-lookup"><span data-stu-id="68579-111">The webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span></span>

## <a name="payload-schema"></a><span data-ttu-id="68579-112">Yükü şeması</span><span class="sxs-lookup"><span data-stu-id="68579-112">Payload schema</span></span>
<span data-ttu-id="68579-113">POST işleminde yer alan JSON yükü yükü 's data.context.activityLog.eventSource alana göre farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="68579-113">The JSON payload contained in the POST operation differs based on the payload's data.context.activityLog.eventSource field.</span></span>

###<a name="common"></a><span data-ttu-id="68579-114">Ortak</span><span class="sxs-lookup"><span data-stu-id="68579-114">Common</span></span>
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "channels": "Operation",
                "correlationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "eventSource": "Administrative",
                "eventTimestamp": "2017-03-29T15:43:08.0019532+00:00",
                "eventDataId": "8195a56a-85de-4663-943e-1a2bf401ad94",
                "level": "Informational",
                "operationName": "Microsoft.Insights/actionGroups/write",
                "operationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "status": "Started",
                "subStatus": "",
                "subscriptionId": "52c65f65-0518-4d37-9719-7dbbfc68c57a",
                "submissionTimestamp": "2017-03-29T15:43:20.3863637+00:00",
                ...
            }
        },
        "properties": {}
    }
}
```
###<a name="administrative"></a><span data-ttu-id="68579-115">Yönetim</span><span class="sxs-lookup"><span data-stu-id="68579-115">Administrative</span></span>
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "authorization": {
                    "action": "Microsoft.Insights/actionGroups/write",
                    "scope": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions"
                },
                "claims": "{...}",
                "caller": "me@contoso.com",
                "description": "",
                "httpRequest": "{...}",
                "resourceId": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions",
                "resourceGroupName": "CONTOSO-TEST",
                "resourceProviderName": "Microsoft.Insights",
                "resourceType": "Microsoft.Insights/actionGroups"
            }
        },
        "properties": {}
    }
}

```
###<a name="servicehealth"></a><span data-ttu-id="68579-116">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="68579-116">ServiceHealth</span></span>
```json
{
    "schemaId": "unknown",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "properties": {
                    "title": "...",
                    "service": "...",
                    "region": "...",
                    "communication": "...",
                    "incidentType": "Incident",
                    "trackingId": "...",
                    "groupId": "...",
                    "impactStartTime": "3/29/2017 3:43:21 PM",
                    "impactMitigationTime": "3/29/2017 3:43:21 PM",
                    "eventCreationTime": "3/29/2017 3:43:21 PM",
                    "impactedServices": "[{...}]",
                    "defaultLanguageTitle": "...",
                    "defaultLanguageContent": "...",
                    "stage": "Active",
                    "communicationId": "...",
                    "version": "0.1"
                }
            }
        },
        "properties": {}
    }
}
```

<span data-ttu-id="68579-117">Belirli şeması hakkında ayrıntılı bilgi için hizmet sistem durumu bildirimi etkinlik günlüğü uyarıları görmek [hizmet durumu bildirimlerine](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="68579-117">For specific schema details on service health notification activity log alerts, see [Service health notifications](monitoring-service-notifications.md).</span></span>

<span data-ttu-id="68579-118">Belirli şeması hakkında ayrıntılı bilgi için diğer tüm etkinlik günlüğü uyarıları görmek [Azure etkinlik günlüğü'ne genel bakış](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="68579-118">For specific schema details on all other activity log alerts, see [Overview of the Azure activity log](monitoring-overview-activity-logs.md).</span></span>

| <span data-ttu-id="68579-119">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="68579-119">Element name</span></span> | <span data-ttu-id="68579-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="68579-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="68579-121">durum</span><span class="sxs-lookup"><span data-stu-id="68579-121">status</span></span> |<span data-ttu-id="68579-122">Ölçüm uyarılar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="68579-122">Used for metric alerts.</span></span> <span data-ttu-id="68579-123">Her zaman "etkinlik günlüğü uyarıları için etkinleştirilmiş" olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="68579-123">Always set to "activated" for activity log alerts.</span></span> |
| <span data-ttu-id="68579-124">bağlam</span><span class="sxs-lookup"><span data-stu-id="68579-124">context</span></span> |<span data-ttu-id="68579-125">Olayın bağlamı.</span><span class="sxs-lookup"><span data-stu-id="68579-125">Context of the event.</span></span> |
| <span data-ttu-id="68579-126">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="68579-126">resourceProviderName</span></span> |<span data-ttu-id="68579-127">Etkilenen kaynağının kaynak sağlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="68579-127">The resource provider of the impacted resource.</span></span> |
| <span data-ttu-id="68579-128">Koşul türü</span><span class="sxs-lookup"><span data-stu-id="68579-128">conditionType</span></span> |<span data-ttu-id="68579-129">Her zaman "olayını."</span><span class="sxs-lookup"><span data-stu-id="68579-129">Always "Event."</span></span> |
| <span data-ttu-id="68579-130">ad</span><span class="sxs-lookup"><span data-stu-id="68579-130">name</span></span> |<span data-ttu-id="68579-131">Uyarı kuralı adı.</span><span class="sxs-lookup"><span data-stu-id="68579-131">Name of the alert rule.</span></span> |
| <span data-ttu-id="68579-132">id</span><span class="sxs-lookup"><span data-stu-id="68579-132">id</span></span> |<span data-ttu-id="68579-133">Uyarının kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="68579-133">Resource ID of the alert.</span></span> |
| <span data-ttu-id="68579-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="68579-134">description</span></span> |<span data-ttu-id="68579-135">Uyarı açıklaması uyarı oluşturulduğunda ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="68579-135">Alert description set when the alert is created.</span></span> |
| <span data-ttu-id="68579-136">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="68579-136">subscriptionId</span></span> |<span data-ttu-id="68579-137">Azure abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="68579-137">Azure subscription ID.</span></span> |
| <span data-ttu-id="68579-138">timestamp</span><span class="sxs-lookup"><span data-stu-id="68579-138">timestamp</span></span> |<span data-ttu-id="68579-139">Olay istek işlenmeden Azure hizmeti tarafından oluşturulduğu saat.</span><span class="sxs-lookup"><span data-stu-id="68579-139">Time at which the event was generated by the Azure service that processed the request.</span></span> |
| <span data-ttu-id="68579-140">resourceId</span><span class="sxs-lookup"><span data-stu-id="68579-140">resourceId</span></span> |<span data-ttu-id="68579-141">Etkilenen kaynağının kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="68579-141">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="68579-142">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="68579-142">resourceGroupName</span></span> |<span data-ttu-id="68579-143">Etkilenen kaynak kaynak grubu adı.</span><span class="sxs-lookup"><span data-stu-id="68579-143">Name of the resource group for the impacted resource.</span></span> |
| <span data-ttu-id="68579-144">properties</span><span class="sxs-lookup"><span data-stu-id="68579-144">properties</span></span> |<span data-ttu-id="68579-145">Kümesi `<Key, Value>` çiftleri (diğer bir deyişle, `Dictionary<String, String>`) olay ayrıntılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="68579-145">Set of `<Key, Value>` pairs (that is, `Dictionary<String, String>`) that includes details about the event.</span></span> |
| <span data-ttu-id="68579-146">Olay</span><span class="sxs-lookup"><span data-stu-id="68579-146">event</span></span> |<span data-ttu-id="68579-147">Olay hakkında meta veriler içeren öğe.</span><span class="sxs-lookup"><span data-stu-id="68579-147">Element that contains metadata about the event.</span></span> |
| <span data-ttu-id="68579-148">Yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="68579-148">authorization</span></span> |<span data-ttu-id="68579-149">Olay rol tabanlı erişim denetimi özellikleri.</span><span class="sxs-lookup"><span data-stu-id="68579-149">The Role-Based Access Control properties of the event.</span></span> <span data-ttu-id="68579-150">Bu özellikler, eylem, rolü ve kapsamı genellikle içerir.</span><span class="sxs-lookup"><span data-stu-id="68579-150">These properties usually include the action, the role, and the scope.</span></span> |
| <span data-ttu-id="68579-151">category</span><span class="sxs-lookup"><span data-stu-id="68579-151">category</span></span> |<span data-ttu-id="68579-152">Olay kategorisi.</span><span class="sxs-lookup"><span data-stu-id="68579-152">Category of the event.</span></span> <span data-ttu-id="68579-153">Yönetim, uyarı, güvenlik, ServiceHealth ve öneri desteklenen değerler içerir.</span><span class="sxs-lookup"><span data-stu-id="68579-153">Supported values include Administrative, Alert, Security, ServiceHealth, and Recommendation.</span></span> |
| <span data-ttu-id="68579-154">Arayan</span><span class="sxs-lookup"><span data-stu-id="68579-154">caller</span></span> |<span data-ttu-id="68579-155">İşlem, UPN Talebi veya kullanılabilirliğine göre SPN talep gerçekleştiren kullanıcı e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="68579-155">Email address of the user who performed the operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="68579-156">Belirli sistem çağrıları için null olabilir.</span><span class="sxs-lookup"><span data-stu-id="68579-156">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="68579-157">correlationId</span><span class="sxs-lookup"><span data-stu-id="68579-157">correlationId</span></span> |<span data-ttu-id="68579-158">Genellikle bir GUID dize biçiminde.</span><span class="sxs-lookup"><span data-stu-id="68579-158">Usually a GUID in string format.</span></span> <span data-ttu-id="68579-159">Correlationıd değeri olaylarla aynı büyük eyleme ait ve genellikle bir correlationıd değeri paylaşın.</span><span class="sxs-lookup"><span data-stu-id="68579-159">Events with correlationId belong to the same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="68579-160">eventDescription</span><span class="sxs-lookup"><span data-stu-id="68579-160">eventDescription</span></span> |<span data-ttu-id="68579-161">Olay açıklaması statik metin.</span><span class="sxs-lookup"><span data-stu-id="68579-161">Static text description of the event.</span></span> |
| <span data-ttu-id="68579-162">eventDataId</span><span class="sxs-lookup"><span data-stu-id="68579-162">eventDataId</span></span> |<span data-ttu-id="68579-163">Olay için benzersiz tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="68579-163">Unique identifier for the event.</span></span> |
| <span data-ttu-id="68579-164">EventSource</span><span class="sxs-lookup"><span data-stu-id="68579-164">eventSource</span></span> |<span data-ttu-id="68579-165">Azure hizmet veya olayı oluşturan altyapı adı.</span><span class="sxs-lookup"><span data-stu-id="68579-165">Name of the Azure service or infrastructure that generated the event.</span></span> |
| <span data-ttu-id="68579-166">httpRequest</span><span class="sxs-lookup"><span data-stu-id="68579-166">httpRequest</span></span> |<span data-ttu-id="68579-167">İstek genellikle clientRequestId, clientIpAddress ve HTTP yöntemini içerir (örneğin, PUT).</span><span class="sxs-lookup"><span data-stu-id="68579-167">The request usually includes the clientRequestId, clientIpAddress, and HTTP method (for example, PUT).</span></span> |
| <span data-ttu-id="68579-168">düzeyi</span><span class="sxs-lookup"><span data-stu-id="68579-168">level</span></span> |<span data-ttu-id="68579-169">Aşağıdaki değerlerden birini: Kritik hata, uyarı, bilgilendirici ve ayrıntılı.</span><span class="sxs-lookup"><span data-stu-id="68579-169">One of the following values: Critical, Error, Warning, Informational, and Verbose.</span></span> |
| <span data-ttu-id="68579-170">Operationıd</span><span class="sxs-lookup"><span data-stu-id="68579-170">operationId</span></span> |<span data-ttu-id="68579-171">Tek bir işlem için karşılık gelen olayları arasında paylaşılan genellikle bir GUID.</span><span class="sxs-lookup"><span data-stu-id="68579-171">Usually a GUID shared among the events corresponding to single operation.</span></span> |
| <span data-ttu-id="68579-172">operationName</span><span class="sxs-lookup"><span data-stu-id="68579-172">operationName</span></span> |<span data-ttu-id="68579-173">İşlemin adı.</span><span class="sxs-lookup"><span data-stu-id="68579-173">Name of the operation.</span></span> |
| <span data-ttu-id="68579-174">properties</span><span class="sxs-lookup"><span data-stu-id="68579-174">properties</span></span> |<span data-ttu-id="68579-175">Olay Özellikleri.</span><span class="sxs-lookup"><span data-stu-id="68579-175">Properties of the event.</span></span> |
| <span data-ttu-id="68579-176">durum</span><span class="sxs-lookup"><span data-stu-id="68579-176">status</span></span> |<span data-ttu-id="68579-177">Dize.</span><span class="sxs-lookup"><span data-stu-id="68579-177">String.</span></span> <span data-ttu-id="68579-178">İşlem durumu.</span><span class="sxs-lookup"><span data-stu-id="68579-178">Status of the operation.</span></span> <span data-ttu-id="68579-179">Ortak değerleri başlatıldı, devam eden, başarılı, başarısız, etkin ve Çözümlenmiş içerir.</span><span class="sxs-lookup"><span data-stu-id="68579-179">Common values include Started, In Progress, Succeeded, Failed, Active, and Resolved.</span></span> |
| <span data-ttu-id="68579-180">alt durum</span><span class="sxs-lookup"><span data-stu-id="68579-180">subStatus</span></span> |<span data-ttu-id="68579-181">Genellikle, karşılık gelen REST çağrısı HTTP durum kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="68579-181">Usually includes the HTTP status code of the corresponding REST call.</span></span> <span data-ttu-id="68579-182">Ayrıca, bir alt durum açıklayan diğer dizeleri de içerebilir.</span><span class="sxs-lookup"><span data-stu-id="68579-182">It might also include other strings that describe a substatus.</span></span> <span data-ttu-id="68579-183">Ortak substatus değerler Tamam (HTTP durum kodu: 200), oluşturulan (HTTP durum kodu: 201), kabul edilen (HTTP durum kodu: 202), Hayır içeriği (HTTP durum kodu: 204), hatalı istek (HTTP durum kodu: 400), bulunamadı (HTTP durum kodu: 404), çakışma (HTTP durum kodu: 409), iç sunucu hatası (HTTP durum kodu: 500), hizmet kullanılamıyor (HTTP durum kodu: 503) ve ağ geçidi zaman aşımı (HTTP durum kodu : 504).</span><span class="sxs-lookup"><span data-stu-id="68579-183">Common substatus values include OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), and Gateway Timeout (HTTP Status Code: 504).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="68579-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="68579-184">Next steps</span></span>
* <span data-ttu-id="68579-185">[Etkinlik günlüğü hakkında daha fazla bilgi](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="68579-185">[Learn more about the activity log](monitoring-overview-activity-logs.md).</span></span>
* <span data-ttu-id="68579-186">[Azure Otomasyon betikleri (Runbook'lar) Azure uyarılar yürütme](http://go.microsoft.com/fwlink/?LinkId=627081).</span><span class="sxs-lookup"><span data-stu-id="68579-186">[Execute Azure automation scripts (Runbooks) on Azure alerts](http://go.microsoft.com/fwlink/?LinkId=627081).</span></span>
* <span data-ttu-id="68579-187">[Twilio aracılığıyla bir SMS gelen Azure uyarı göndermek için bir mantıksal uygulama kullanmak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="68579-187">[Use a logic app to send an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="68579-188">Bu örnek için ölçüm uyarıları olmakla birlikte, bir etkinlik günlüğü uyarı ile çalışmak için değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="68579-188">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
* <span data-ttu-id="68579-189">[Bir Azure uyarıdan Slack ileti göndermek için bir mantıksal uygulama kullanmak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="68579-189">[Use a logic app to send a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="68579-190">Bu örnek için ölçüm uyarıları olmakla birlikte, bir etkinlik günlüğü uyarı ile çalışmak için değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="68579-190">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
* <span data-ttu-id="68579-191">[Bir Azure uyarıdan bir Azure kuyruğuna ileti göndermek için bir mantıksal uygulama kullanmak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="68579-191">[Use a logic app to send a message to an Azure queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="68579-192">Bu örnek için ölçüm uyarıları olmakla birlikte, bir etkinlik günlüğü uyarı ile çalışmak için değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="68579-192">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
