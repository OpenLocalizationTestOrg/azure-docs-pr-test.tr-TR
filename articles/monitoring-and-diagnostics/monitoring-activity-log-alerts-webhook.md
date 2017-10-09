---
title: "Etkinlik günlüğü uyarıları kullanılan aaaUnderstand hello Web kancası şema | Microsoft Docs"
description: "Merhaba etkinlik günlüğü uyarı etkinleştirdiğinde tooa Web kancası URL'si gönderilen JSON Hello şeması hakkında bilgi edinin."
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
ms.openlocfilehash: 75562e0589222d3e392ea73eacfd7414a422d115
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a><span data-ttu-id="bd70b-103">Azure etkinlik günlüğü uyarılar için Web kancaları</span><span class="sxs-lookup"><span data-stu-id="bd70b-103">Webhooks for Azure activity log alerts</span></span>
<span data-ttu-id="bd70b-104">Bir eylem grubu hello tanımının bir parçası olarak, Web kancası uç noktaları tooreceive etkinlik günlüğü uyarı bildirimleri yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd70b-104">As part of hello definition of an action group, you can configure webhook endpoints tooreceive activity log alert notifications.</span></span> <span data-ttu-id="bd70b-105">Web kancası ile bu bildirimleri tooother sistemleri işlem sonrası ya da özel eylemler için yönlendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd70b-105">With webhooks, you can route these notifications tooother systems for post-processing or custom actions.</span></span> <span data-ttu-id="bd70b-106">Bu makalede hello HTTP POST tooa gibi görünüyor Web kancası için hangi hello yükü gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="bd70b-106">This article shows what hello payload for hello HTTP POST tooa webhook looks like.</span></span>

<span data-ttu-id="bd70b-107">Etkinlik günlüğü uyarılar hakkında daha fazla bilgi için bkz. nasıl çok[Azure etkinlik günlüğü uyarı oluşturma](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="bd70b-107">For more information on activity log alerts, see how too[create Azure activity log alerts](monitoring-activity-log-alerts.md).</span></span>

<span data-ttu-id="bd70b-108">Eylem grupları hakkında daha fazla bilgi için bkz. nasıl çok[Eylem grupları oluşturma](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="bd70b-108">For information on action groups, see how too[create action groups](monitoring-action-groups.md).</span></span>

## <a name="authenticate-hello-webhook"></a><span data-ttu-id="bd70b-109">Merhaba Web kancası kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="bd70b-109">Authenticate hello webhook</span></span>
<span data-ttu-id="bd70b-110">Merhaba Web kancası kimlik doğrulaması için isteğe bağlı olarak belirteç tabanlı bir yetkilendirme kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd70b-110">hello webhook can optionally use token-based authorization for authentication.</span></span> <span data-ttu-id="bd70b-111">URI kaydedilir belirteci Kimliğine sahip, örneğin, Web kancası hello `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span><span class="sxs-lookup"><span data-stu-id="bd70b-111">hello webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span></span>

## <a name="payload-schema"></a><span data-ttu-id="bd70b-112">Yükü şeması</span><span class="sxs-lookup"><span data-stu-id="bd70b-112">Payload schema</span></span>
<span data-ttu-id="bd70b-113">Merhaba POST işlemine bulunan hello JSON yükü hello yükü'nın data.context.activityLog.eventSource alanında bulunan göre farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="bd70b-113">hello JSON payload contained in hello POST operation differs based on hello payload's data.context.activityLog.eventSource field.</span></span>

###<a name="common"></a><span data-ttu-id="bd70b-114">Ortak</span><span class="sxs-lookup"><span data-stu-id="bd70b-114">Common</span></span>
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
###<a name="administrative"></a><span data-ttu-id="bd70b-115">Yönetim</span><span class="sxs-lookup"><span data-stu-id="bd70b-115">Administrative</span></span>
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
###<a name="servicehealth"></a><span data-ttu-id="bd70b-116">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="bd70b-116">ServiceHealth</span></span>
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

<span data-ttu-id="bd70b-117">Belirli şeması hakkında ayrıntılı bilgi için hizmet sistem durumu bildirimi etkinlik günlüğü uyarıları görmek [hizmet durumu bildirimlerine](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="bd70b-117">For specific schema details on service health notification activity log alerts, see [Service health notifications](monitoring-service-notifications.md).</span></span>

<span data-ttu-id="bd70b-118">Belirli şeması hakkında ayrıntılı bilgi için diğer tüm etkinlik günlüğü uyarıları görmek [hello Azure etkinlik günlüğü'ne genel bakış](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="bd70b-118">For specific schema details on all other activity log alerts, see [Overview of hello Azure activity log](monitoring-overview-activity-logs.md).</span></span>

| <span data-ttu-id="bd70b-119">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="bd70b-119">Element name</span></span> | <span data-ttu-id="bd70b-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bd70b-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bd70b-121">durum</span><span class="sxs-lookup"><span data-stu-id="bd70b-121">status</span></span> |<span data-ttu-id="bd70b-122">Ölçüm uyarılar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bd70b-122">Used for metric alerts.</span></span> <span data-ttu-id="bd70b-123">Her zaman "çok etkinlik günlüğü uyarıları için etkinleştirilmiş" ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="bd70b-123">Always set too"activated" for activity log alerts.</span></span> |
| <span data-ttu-id="bd70b-124">bağlam</span><span class="sxs-lookup"><span data-stu-id="bd70b-124">context</span></span> |<span data-ttu-id="bd70b-125">Merhaba olay bağlamı.</span><span class="sxs-lookup"><span data-stu-id="bd70b-125">Context of hello event.</span></span> |
| <span data-ttu-id="bd70b-126">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="bd70b-126">resourceProviderName</span></span> |<span data-ttu-id="bd70b-127">Merhaba Hello kaynak sağlayıcısı kaynak etkilenmiş.</span><span class="sxs-lookup"><span data-stu-id="bd70b-127">hello resource provider of hello impacted resource.</span></span> |
| <span data-ttu-id="bd70b-128">Koşul türü</span><span class="sxs-lookup"><span data-stu-id="bd70b-128">conditionType</span></span> |<span data-ttu-id="bd70b-129">Her zaman "olayını."</span><span class="sxs-lookup"><span data-stu-id="bd70b-129">Always "Event."</span></span> |
| <span data-ttu-id="bd70b-130">ad</span><span class="sxs-lookup"><span data-stu-id="bd70b-130">name</span></span> |<span data-ttu-id="bd70b-131">Merhaba uyarı kuralının adı.</span><span class="sxs-lookup"><span data-stu-id="bd70b-131">Name of hello alert rule.</span></span> |
| <span data-ttu-id="bd70b-132">id</span><span class="sxs-lookup"><span data-stu-id="bd70b-132">id</span></span> |<span data-ttu-id="bd70b-133">Merhaba uyarı kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="bd70b-133">Resource ID of hello alert.</span></span> |
| <span data-ttu-id="bd70b-134">açıklama</span><span class="sxs-lookup"><span data-stu-id="bd70b-134">description</span></span> |<span data-ttu-id="bd70b-135">Uyarı açıklaması Hello uyarı oluşturulduğunda ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="bd70b-135">Alert description set when hello alert is created.</span></span> |
| <span data-ttu-id="bd70b-136">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="bd70b-136">subscriptionId</span></span> |<span data-ttu-id="bd70b-137">Azure abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="bd70b-137">Azure subscription ID.</span></span> |
| <span data-ttu-id="bd70b-138">timestamp</span><span class="sxs-lookup"><span data-stu-id="bd70b-138">timestamp</span></span> |<span data-ttu-id="bd70b-139">Hangi hello olay hello hello istek işlenmeden Azure hizmeti tarafından oluşturulan saat.</span><span class="sxs-lookup"><span data-stu-id="bd70b-139">Time at which hello event was generated by hello Azure service that processed hello request.</span></span> |
| <span data-ttu-id="bd70b-140">resourceId</span><span class="sxs-lookup"><span data-stu-id="bd70b-140">resourceId</span></span> |<span data-ttu-id="bd70b-141">Kaynak Kimliğini hello kaynak etkilenmiş.</span><span class="sxs-lookup"><span data-stu-id="bd70b-141">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="bd70b-142">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="bd70b-142">resourceGroupName</span></span> |<span data-ttu-id="bd70b-143">Merhaba hello kaynak grubunun adı, kaynak etkilenmiş.</span><span class="sxs-lookup"><span data-stu-id="bd70b-143">Name of hello resource group for hello impacted resource.</span></span> |
| <span data-ttu-id="bd70b-144">properties</span><span class="sxs-lookup"><span data-stu-id="bd70b-144">properties</span></span> |<span data-ttu-id="bd70b-145">Kümesi `<Key, Value>` çiftleri (diğer bir deyişle, `Dictionary<String, String>`) hello olay ayrıntılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="bd70b-145">Set of `<Key, Value>` pairs (that is, `Dictionary<String, String>`) that includes details about hello event.</span></span> |
| <span data-ttu-id="bd70b-146">Olay</span><span class="sxs-lookup"><span data-stu-id="bd70b-146">event</span></span> |<span data-ttu-id="bd70b-147">Merhaba olay hakkında meta veriler içeren öğe.</span><span class="sxs-lookup"><span data-stu-id="bd70b-147">Element that contains metadata about hello event.</span></span> |
| <span data-ttu-id="bd70b-148">Yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="bd70b-148">authorization</span></span> |<span data-ttu-id="bd70b-149">Merhaba olay Hello rol tabanlı erişim denetimi özellikleri.</span><span class="sxs-lookup"><span data-stu-id="bd70b-149">hello Role-Based Access Control properties of hello event.</span></span> <span data-ttu-id="bd70b-150">Bu özellikler genellikle hello eylem, hello rolü ve hello kapsamı içerir.</span><span class="sxs-lookup"><span data-stu-id="bd70b-150">These properties usually include hello action, hello role, and hello scope.</span></span> |
| <span data-ttu-id="bd70b-151">category</span><span class="sxs-lookup"><span data-stu-id="bd70b-151">category</span></span> |<span data-ttu-id="bd70b-152">Merhaba olay kategorisi.</span><span class="sxs-lookup"><span data-stu-id="bd70b-152">Category of hello event.</span></span> <span data-ttu-id="bd70b-153">Yönetim, uyarı, güvenlik, ServiceHealth ve öneri desteklenen değerler içerir.</span><span class="sxs-lookup"><span data-stu-id="bd70b-153">Supported values include Administrative, Alert, Security, ServiceHealth, and Recommendation.</span></span> |
| <span data-ttu-id="bd70b-154">Arayan</span><span class="sxs-lookup"><span data-stu-id="bd70b-154">caller</span></span> |<span data-ttu-id="bd70b-155">Merhaba işlemi, UPN Talebi veya kullanılabilirliğine göre SPN talep gerçekleştiren hello kullanıcının e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="bd70b-155">Email address of hello user who performed hello operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="bd70b-156">Belirli sistem çağrıları için null olabilir.</span><span class="sxs-lookup"><span data-stu-id="bd70b-156">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="bd70b-157">correlationId</span><span class="sxs-lookup"><span data-stu-id="bd70b-157">correlationId</span></span> |<span data-ttu-id="bd70b-158">Genellikle bir GUID dize biçiminde.</span><span class="sxs-lookup"><span data-stu-id="bd70b-158">Usually a GUID in string format.</span></span> <span data-ttu-id="bd70b-159">Correlationıd değeri olaylarla ait toohello aynı büyük eylemi ve genellikle bir correlationıd değeri paylaşın.</span><span class="sxs-lookup"><span data-stu-id="bd70b-159">Events with correlationId belong toohello same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="bd70b-160">eventDescription</span><span class="sxs-lookup"><span data-stu-id="bd70b-160">eventDescription</span></span> |<span data-ttu-id="bd70b-161">Merhaba Olay açıklaması statik metin.</span><span class="sxs-lookup"><span data-stu-id="bd70b-161">Static text description of hello event.</span></span> |
| <span data-ttu-id="bd70b-162">eventDataId</span><span class="sxs-lookup"><span data-stu-id="bd70b-162">eventDataId</span></span> |<span data-ttu-id="bd70b-163">Merhaba olay için benzersiz tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="bd70b-163">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="bd70b-164">EventSource</span><span class="sxs-lookup"><span data-stu-id="bd70b-164">eventSource</span></span> |<span data-ttu-id="bd70b-165">Hello Azure hizmetine veya altyapı oluşturulan hello olayın adı.</span><span class="sxs-lookup"><span data-stu-id="bd70b-165">Name of hello Azure service or infrastructure that generated hello event.</span></span> |
| <span data-ttu-id="bd70b-166">httpRequest</span><span class="sxs-lookup"><span data-stu-id="bd70b-166">httpRequest</span></span> |<span data-ttu-id="bd70b-167">Merhaba istek genellikle hello clientRequestId, clientIpAddress ve HTTP yöntemini içerir (örneğin, PUT).</span><span class="sxs-lookup"><span data-stu-id="bd70b-167">hello request usually includes hello clientRequestId, clientIpAddress, and HTTP method (for example, PUT).</span></span> |
| <span data-ttu-id="bd70b-168">düzeyi</span><span class="sxs-lookup"><span data-stu-id="bd70b-168">level</span></span> |<span data-ttu-id="bd70b-169">Değerleri aşağıdaki hello birini: Kritik hata, uyarı, bilgilendirici ve ayrıntılı.</span><span class="sxs-lookup"><span data-stu-id="bd70b-169">One of hello following values: Critical, Error, Warning, Informational, and Verbose.</span></span> |
| <span data-ttu-id="bd70b-170">Operationıd</span><span class="sxs-lookup"><span data-stu-id="bd70b-170">operationId</span></span> |<span data-ttu-id="bd70b-171">Toosingle işlemi karşılık gelen hello olaylar arasında paylaşılan genellikle bir GUID.</span><span class="sxs-lookup"><span data-stu-id="bd70b-171">Usually a GUID shared among hello events corresponding toosingle operation.</span></span> |
| <span data-ttu-id="bd70b-172">operationName</span><span class="sxs-lookup"><span data-stu-id="bd70b-172">operationName</span></span> |<span data-ttu-id="bd70b-173">Merhaba işlemin adı.</span><span class="sxs-lookup"><span data-stu-id="bd70b-173">Name of hello operation.</span></span> |
| <span data-ttu-id="bd70b-174">properties</span><span class="sxs-lookup"><span data-stu-id="bd70b-174">properties</span></span> |<span data-ttu-id="bd70b-175">Merhaba olay özellikleri.</span><span class="sxs-lookup"><span data-stu-id="bd70b-175">Properties of hello event.</span></span> |
| <span data-ttu-id="bd70b-176">durum</span><span class="sxs-lookup"><span data-stu-id="bd70b-176">status</span></span> |<span data-ttu-id="bd70b-177">Dize.</span><span class="sxs-lookup"><span data-stu-id="bd70b-177">String.</span></span> <span data-ttu-id="bd70b-178">Merhaba işlem durumu.</span><span class="sxs-lookup"><span data-stu-id="bd70b-178">Status of hello operation.</span></span> <span data-ttu-id="bd70b-179">Ortak değerleri başlatıldı, devam eden, başarılı, başarısız, etkin ve Çözümlenmiş içerir.</span><span class="sxs-lookup"><span data-stu-id="bd70b-179">Common values include Started, In Progress, Succeeded, Failed, Active, and Resolved.</span></span> |
| <span data-ttu-id="bd70b-180">alt durum</span><span class="sxs-lookup"><span data-stu-id="bd70b-180">subStatus</span></span> |<span data-ttu-id="bd70b-181">Genellikle hello karşılık gelen REST çağrısı hello HTTP durum kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="bd70b-181">Usually includes hello HTTP status code of hello corresponding REST call.</span></span> <span data-ttu-id="bd70b-182">Ayrıca, bir alt durum açıklayan diğer dizeleri de içerebilir.</span><span class="sxs-lookup"><span data-stu-id="bd70b-182">It might also include other strings that describe a substatus.</span></span> <span data-ttu-id="bd70b-183">Ortak substatus değerler Tamam (HTTP durum kodu: 200), oluşturulan (HTTP durum kodu: 201), kabul edilen (HTTP durum kodu: 202), Hayır içeriği (HTTP durum kodu: 204), hatalı istek (HTTP durum kodu: 400), bulunamadı (HTTP durum kodu: 404), çakışma (HTTP durum kodu: 409), iç sunucu hatası (HTTP durum kodu: 500), hizmet kullanılamıyor (HTTP durum kodu: 503) ve ağ geçidi zaman aşımı (HTTP durum kodu : 504).</span><span class="sxs-lookup"><span data-stu-id="bd70b-183">Common substatus values include OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), and Gateway Timeout (HTTP Status Code: 504).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bd70b-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bd70b-184">Next steps</span></span>
* <span data-ttu-id="bd70b-185">[Merhaba etkinlik günlüğü hakkında daha fazla bilgi](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="bd70b-185">[Learn more about hello activity log](monitoring-overview-activity-logs.md).</span></span>
* <span data-ttu-id="bd70b-186">[Azure Otomasyon betikleri (Runbook'lar) Azure uyarılar yürütme](http://go.microsoft.com/fwlink/?LinkId=627081).</span><span class="sxs-lookup"><span data-stu-id="bd70b-186">[Execute Azure automation scripts (Runbooks) on Azure alerts](http://go.microsoft.com/fwlink/?LinkId=627081).</span></span>
* <span data-ttu-id="bd70b-187">[Bir Azure uyarıdan mantığı uygulama toosend Twilio aracılığıyla bir SMS kullanmak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="bd70b-187">[Use a logic app toosend an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="bd70b-188">Bu örnekte ölçüm uyarıları, ancak bir etkinlik günlüğü uyarı ile değiştirilmiş toowork olabilir.</span><span class="sxs-lookup"><span data-stu-id="bd70b-188">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
* <span data-ttu-id="bd70b-189">[Bir mantıksal uygulama toosend Azure uyarı Slack iletiden kullanmak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="bd70b-189">[Use a logic app toosend a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="bd70b-190">Bu örnekte ölçüm uyarıları, ancak bir etkinlik günlüğü uyarı ile değiştirilmiş toowork olabilir.</span><span class="sxs-lookup"><span data-stu-id="bd70b-190">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
* <span data-ttu-id="bd70b-191">[İleti tooan Azure kuyruk Azure bir uyarıdan mantığı uygulama toosend kullanmak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="bd70b-191">[Use a logic app toosend a message tooan Azure queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="bd70b-192">Bu örnekte ölçüm uyarıları, ancak bir etkinlik günlüğü uyarı ile değiştirilmiş toowork olabilir.</span><span class="sxs-lookup"><span data-stu-id="bd70b-192">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
