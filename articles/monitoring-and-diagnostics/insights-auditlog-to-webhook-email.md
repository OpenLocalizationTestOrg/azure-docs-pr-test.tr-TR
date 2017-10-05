---
title: "Bir Web kancası Azure etkinlik günlüğü uyarılar çağrı | Microsoft Docs"
description: "Rota etkinlik günlüğü olaylarını özel eylemler için diğer hizmetler. Örneğin SMS gönder, hatalar oturum veya sohbet ve mesajlaşma hizmeti üzerinden bir takım bildirin."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 64d333d1-7f37-4a00-9d16-dda6e69a113b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: johnkem
ms.openlocfilehash: 341ab32ad0ec691285fbf1537ee298ab30156a5d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="call-a-webhook-on-azure-activity-log-alerts"></a><span data-ttu-id="2a044-104">Bir Web kancası Azure etkinlik günlüğü uyarılar çağırın</span><span class="sxs-lookup"><span data-stu-id="2a044-104">Call a webhook on Azure Activity Log alerts</span></span>
<span data-ttu-id="2a044-105">Web kancası işlem sonrası ya da özel eylemler için diğer sistemlere Azure bir uyarı bildirimine yol olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a044-105">Webhooks allow you to route an Azure alert notification to other systems for post-processing or custom actions.</span></span> <span data-ttu-id="2a044-106">SMS gönder, hatalar oturum, sohbet ve mesajlaşma Servisleri üzerinden bir takım bildirmek veya başka eylemler herhangi bir sayıda yapmak hizmetlere yönlendirmek için bir uyarı durumunda bir Web kancası kullanın.</span><span class="sxs-lookup"><span data-stu-id="2a044-106">You can use a webhook on an alert to route it to services that send SMS, log bugs, notify a team via chat/messaging services, or do any number of other actions.</span></span> <span data-ttu-id="2a044-107">Bu makalede, Azure etkinlik günlüğü uyarı ateşlenir olduğunda çağrılacak bir Web kancası ayarlanacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="2a044-107">This article describes how to set a webhook to be called when an Azure Activity Log alert fires.</span></span> <span data-ttu-id="2a044-108">Ayrıca, bir Web kancası için HTTP POST için yükü nasıl göründüğünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="2a044-108">It also shows what the payload for the HTTP POST to a webhook looks like.</span></span> <span data-ttu-id="2a044-109">Kurulum ve bir Azure ölçüm uyarı şeması hakkında bilgi için [bunun yerine bu sayfaya bakın](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="2a044-109">For information on the setup and schema for an Azure metric alert, [see this page instead](insights-webhooks-alerts.md).</span></span> <span data-ttu-id="2a044-110">Etkinleştirildiğinde bir e-posta göndermek için bir etkinlik günlüğü alarm de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a044-110">You can also set up an Activity Log alert to send email when activated.</span></span>

> [!NOTE]
> <span data-ttu-id="2a044-111">Bu özellik şu anda önizlemede ve belirli bir noktada gelecekte kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="2a044-111">This feature is currently in preview and will be removed at some point in the future.</span></span>
>
>

<span data-ttu-id="2a044-112">Bir etkinlik günlüğü uyarı kullanarak ayarlayabilirsiniz [Azure PowerShell cmdlet'leri](insights-powershell-samples.md#create-metric-alerts), [platformlar arası CLI](insights-cli-samples.md#work-with-alerts), veya [Azure İzleyici REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span><span class="sxs-lookup"><span data-stu-id="2a044-112">You can set up an Activity Log alert using the [Azure PowerShell Cmdlets](insights-powershell-samples.md#create-metric-alerts), [Cross-Platform CLI](insights-cli-samples.md#work-with-alerts), or [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span></span> <span data-ttu-id="2a044-113">Şu anda bir Azure portalını kullanarak ayarlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="2a044-113">Currently, you cannot set one up using the Azure portal.</span></span>

## <a name="authenticating-the-webhook"></a><span data-ttu-id="2a044-114">Web kancası kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="2a044-114">Authenticating the webhook</span></span>
<span data-ttu-id="2a044-115">Web kancası bu yöntemlerden birini kullanarak doğrulayabilir:</span><span class="sxs-lookup"><span data-stu-id="2a044-115">The webhook can authenticate using either of these methods:</span></span>

1. <span data-ttu-id="2a044-116">**Belirteç tabanlı bir yetkilendirme** -URI kaydedilir belirteci Kimliğine sahip, örneğin, Web kancası`https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span><span class="sxs-lookup"><span data-stu-id="2a044-116">**Token-based authorization** - The webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span></span>
2. <span data-ttu-id="2a044-117">**Temel yetkilendirme** -URI kaydedilir bir kullanıcı adı ve parola, örneğin, Web kancası`https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span><span class="sxs-lookup"><span data-stu-id="2a044-117">**Basic authorization** - The webhook URI is saved with a username and password, for example, `https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span></span>

## <a name="payload-schema"></a><span data-ttu-id="2a044-118">Yükü şeması</span><span class="sxs-lookup"><span data-stu-id="2a044-118">Payload schema</span></span>
<span data-ttu-id="2a044-119">GÖNDERME işlemini aşağıdaki JSON yükü ve tüm etkinlik günlüğü tabanlı uyarılar için şema içerir.</span><span class="sxs-lookup"><span data-stu-id="2a044-119">The POST operation contains the following JSON payload and schema for all Activity Log-based alerts.</span></span> <span data-ttu-id="2a044-120">Bu şemayı ölçüm tabanlı uyarılar tarafından kullanılan benzer.</span><span class="sxs-lookup"><span data-stu-id="2a044-120">This schema is similar to the one used by metric-based alerts.</span></span>

```
{
        "status": "Activated",
        "context": {
                "resourceProviderName": "Microsoft.Web",
                "event": {
                        "$type": "Microsoft.WindowsAzure.Management.Monitoring.Automation.Notifications.GenericNotifications.Datacontracts.InstanceEventContext, Microsoft.WindowsAzure.Management.Mon.Automation",
                        "authorization": {
                                "action": "Microsoft.Web/sites/start/action",
                                "scope": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest"
                        },
                        "eventDataId": "327caaca-08d7-41b1-86d8-27d0a7adb92d",
                        "category": "Administrative",
                        "caller": "myname@mycompany.com",
                        "httpRequest": {
                                "clientRequestId": "f58cead8-c9ed-43af-8710-55e64def208d",
                                "clientIpAddress": "104.43.166.155",
                                "method": "POST"
                        },
                        "status": "Succeeded",
                        "subStatus": "OK",
                        "level": "Informational",
                        "correlationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "eventDescription": "",
                        "operationName": "Microsoft.Web/sites/start/action",
                        "operationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "properties": {
                                "$type": "Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage",
                                "statusCode": "OK",
                                "serviceRequestId": "f7716681-496a-4f5c-8d14-d564bcf54714"
                        }
                },
                "timestamp": "Friday, March 11, 2016 9:13:23 PM",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/alertonevent2",
                "name": "alertonevent2",
                "description": "test alert on event start",
                "conditionType": "Event",
                "subscriptionId": "s1",
                "resourceId": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest",
                "resourceGroupName": "rg1"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```

| <span data-ttu-id="2a044-121">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="2a044-121">Element Name</span></span> | <span data-ttu-id="2a044-122">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2a044-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2a044-123">durum</span><span class="sxs-lookup"><span data-stu-id="2a044-123">status</span></span> |<span data-ttu-id="2a044-124">Ölçüm uyarılar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2a044-124">Used for metric alerts.</span></span> <span data-ttu-id="2a044-125">Her zaman "etkin" için etkinlik günlüğü Uyarıları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2a044-125">Always set to "activated" for Activity Log alerts.</span></span> |
| <span data-ttu-id="2a044-126">bağlam</span><span class="sxs-lookup"><span data-stu-id="2a044-126">context</span></span> |<span data-ttu-id="2a044-127">Olayın bağlamı.</span><span class="sxs-lookup"><span data-stu-id="2a044-127">Context of the event.</span></span> |
| <span data-ttu-id="2a044-128">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="2a044-128">resourceProviderName</span></span> |<span data-ttu-id="2a044-129">Etkilenen kaynağının kaynak sağlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="2a044-129">The resource provider of the impacted resource.</span></span> |
| <span data-ttu-id="2a044-130">Koşul türü</span><span class="sxs-lookup"><span data-stu-id="2a044-130">conditionType</span></span> |<span data-ttu-id="2a044-131">Her zaman "olayını."</span><span class="sxs-lookup"><span data-stu-id="2a044-131">Always "Event."</span></span> |
| <span data-ttu-id="2a044-132">ad</span><span class="sxs-lookup"><span data-stu-id="2a044-132">name</span></span> |<span data-ttu-id="2a044-133">Uyarı kuralı adı.</span><span class="sxs-lookup"><span data-stu-id="2a044-133">Name of the alert rule.</span></span> |
| <span data-ttu-id="2a044-134">id</span><span class="sxs-lookup"><span data-stu-id="2a044-134">id</span></span> |<span data-ttu-id="2a044-135">Uyarının kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="2a044-135">Resource ID of the alert.</span></span> |
| <span data-ttu-id="2a044-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2a044-136">description</span></span> |<span data-ttu-id="2a044-137">Uyarı oluşturulması sırasında uyarı açıklaması olarak ayarla.</span><span class="sxs-lookup"><span data-stu-id="2a044-137">Alert description as set during creation of the alert.</span></span> |
| <span data-ttu-id="2a044-138">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="2a044-138">subscriptionId</span></span> |<span data-ttu-id="2a044-139">Azure abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="2a044-139">Azure Subscription ID.</span></span> |
| <span data-ttu-id="2a044-140">timestamp</span><span class="sxs-lookup"><span data-stu-id="2a044-140">timestamp</span></span> |<span data-ttu-id="2a044-141">Olay istek işlenmeden Azure hizmeti tarafından oluşturulduğu saat.</span><span class="sxs-lookup"><span data-stu-id="2a044-141">Time at which the event was generated by the Azure service that processed the request.</span></span> |
| <span data-ttu-id="2a044-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="2a044-142">resourceId</span></span> |<span data-ttu-id="2a044-143">Etkilenen kaynağının kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="2a044-143">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="2a044-144">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="2a044-144">resourceGroupName</span></span> |<span data-ttu-id="2a044-145">Etkilenen kaynak için kaynak grubunun adı</span><span class="sxs-lookup"><span data-stu-id="2a044-145">Name of the resource group for the impacted resource</span></span> |
| <span data-ttu-id="2a044-146">properties</span><span class="sxs-lookup"><span data-stu-id="2a044-146">properties</span></span> |<span data-ttu-id="2a044-147">Kümesi `<Key, Value>` çiftleri (yani `Dictionary<String, String>`) olay ayrıntılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="2a044-147">Set of `<Key, Value>` pairs (i.e. `Dictionary<String, String>`) that includes details about the event.</span></span> |
| <span data-ttu-id="2a044-148">Olay</span><span class="sxs-lookup"><span data-stu-id="2a044-148">event</span></span> |<span data-ttu-id="2a044-149">Olayla ilgili meta verileri içeren öğe.</span><span class="sxs-lookup"><span data-stu-id="2a044-149">Element containing metadata about the event.</span></span> |
| <span data-ttu-id="2a044-150">Yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="2a044-150">authorization</span></span> |<span data-ttu-id="2a044-151">Olay RBAC özellikleri.</span><span class="sxs-lookup"><span data-stu-id="2a044-151">The RBAC properties of the event.</span></span> <span data-ttu-id="2a044-152">Bunlar genellikle "eylem", "rol" ve "scope." içerir</span><span class="sxs-lookup"><span data-stu-id="2a044-152">These usually include the “action”, “role” and the “scope.”</span></span> |
| <span data-ttu-id="2a044-153">category</span><span class="sxs-lookup"><span data-stu-id="2a044-153">category</span></span> |<span data-ttu-id="2a044-154">Olay kategorisi.</span><span class="sxs-lookup"><span data-stu-id="2a044-154">Category of the event.</span></span> <span data-ttu-id="2a044-155">Desteklenen değerler: yönetici, uyarı, güvenlik, ServiceHealth, öneri.</span><span class="sxs-lookup"><span data-stu-id="2a044-155">Supported values include: Administrative, Alert, Security, ServiceHealth, Recommendation.</span></span> |
| <span data-ttu-id="2a044-156">Arayan</span><span class="sxs-lookup"><span data-stu-id="2a044-156">caller</span></span> |<span data-ttu-id="2a044-157">İşlem, UPN Talebi veya kullanılabilirliğine göre SPN talep gerçekleştiren kullanıcı e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="2a044-157">Email address of the user who performed the operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="2a044-158">Belirli sistem çağrıları için null olabilir.</span><span class="sxs-lookup"><span data-stu-id="2a044-158">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="2a044-159">correlationId</span><span class="sxs-lookup"><span data-stu-id="2a044-159">correlationId</span></span> |<span data-ttu-id="2a044-160">Genellikle bir GUID dize biçiminde.</span><span class="sxs-lookup"><span data-stu-id="2a044-160">Usually a GUID in string format.</span></span> <span data-ttu-id="2a044-161">Correlationıd değeri olaylarla aynı büyük eyleme ait ve genellikle bir correlationıd değeri paylaşın.</span><span class="sxs-lookup"><span data-stu-id="2a044-161">Events with correlationId belong to the same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="2a044-162">eventDescription</span><span class="sxs-lookup"><span data-stu-id="2a044-162">eventDescription</span></span> |<span data-ttu-id="2a044-163">Olay açıklaması statik metin.</span><span class="sxs-lookup"><span data-stu-id="2a044-163">Static text description of the event.</span></span> |
| <span data-ttu-id="2a044-164">eventDataId</span><span class="sxs-lookup"><span data-stu-id="2a044-164">eventDataId</span></span> |<span data-ttu-id="2a044-165">Olay için benzersiz tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="2a044-165">Unique identifier for the event.</span></span> |
| <span data-ttu-id="2a044-166">EventSource</span><span class="sxs-lookup"><span data-stu-id="2a044-166">eventSource</span></span> |<span data-ttu-id="2a044-167">Azure hizmet veya olayı oluşturan altyapı adı.</span><span class="sxs-lookup"><span data-stu-id="2a044-167">Name of the Azure service or infrastructure that generated the event.</span></span> |
| <span data-ttu-id="2a044-168">httpRequest</span><span class="sxs-lookup"><span data-stu-id="2a044-168">httpRequest</span></span> |<span data-ttu-id="2a044-169">Genellikle "clientRequestId", "clientIpAddress" ve "yöntemi" içerir (örneğin PUT HTTP yöntemi).</span><span class="sxs-lookup"><span data-stu-id="2a044-169">Usually includes the “clientRequestId”, “clientIpAddress” and “method” (HTTP method e.g. PUT).</span></span> |
| <span data-ttu-id="2a044-170">düzeyi</span><span class="sxs-lookup"><span data-stu-id="2a044-170">level</span></span> |<span data-ttu-id="2a044-171">Aşağıdaki değerlerden birini: "Kritik", "Error"Uyarı",", "Bilgi" ve "Ayrıntılı."</span><span class="sxs-lookup"><span data-stu-id="2a044-171">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose.”</span></span> |
| <span data-ttu-id="2a044-172">Operationıd</span><span class="sxs-lookup"><span data-stu-id="2a044-172">operationId</span></span> |<span data-ttu-id="2a044-173">Tek bir işlem için karşılık gelen olayları arasında paylaşılan genellikle bir GUID.</span><span class="sxs-lookup"><span data-stu-id="2a044-173">Usually a GUID shared among the events corresponding to single operation.</span></span> |
| <span data-ttu-id="2a044-174">operationName</span><span class="sxs-lookup"><span data-stu-id="2a044-174">operationName</span></span> |<span data-ttu-id="2a044-175">İşlemin adı.</span><span class="sxs-lookup"><span data-stu-id="2a044-175">Name of the operation.</span></span> |
| <span data-ttu-id="2a044-176">properties</span><span class="sxs-lookup"><span data-stu-id="2a044-176">properties</span></span> |<span data-ttu-id="2a044-177">Olay Özellikleri.</span><span class="sxs-lookup"><span data-stu-id="2a044-177">Properties of the event.</span></span> |
| <span data-ttu-id="2a044-178">durum</span><span class="sxs-lookup"><span data-stu-id="2a044-178">status</span></span> |<span data-ttu-id="2a044-179">Dize.</span><span class="sxs-lookup"><span data-stu-id="2a044-179">String.</span></span> <span data-ttu-id="2a044-180">İşlem durumu.</span><span class="sxs-lookup"><span data-stu-id="2a044-180">Status of the operation.</span></span> <span data-ttu-id="2a044-181">Genel değerler şunlardır: "Başlatıldı", "Sürüyor", "Başarılı", "Başarısız", "Active", "Çözülmüş".</span><span class="sxs-lookup"><span data-stu-id="2a044-181">Common values include: "Started", "In Progress", "Succeeded", "Failed", "Active", "Resolved".</span></span> |
| <span data-ttu-id="2a044-182">alt durum</span><span class="sxs-lookup"><span data-stu-id="2a044-182">subStatus</span></span> |<span data-ttu-id="2a044-183">Genellikle, karşılık gelen REST çağrısı HTTP durum kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="2a044-183">Usually includes the HTTP status code of the corresponding REST call.</span></span> <span data-ttu-id="2a044-184">Ayrıca, bir alt durum açıklayan diğer dizeleri de içerebilir.</span><span class="sxs-lookup"><span data-stu-id="2a044-184">It might also include other strings describing a substatus.</span></span> <span data-ttu-id="2a044-185">Ortak alt durum değerleri şunları içerir: Tamam (HTTP durum kodu: 200), oluşturulan (HTTP durum kodu: 201), kabul edilen (HTTP durum kodu: 202), Hayır içeriği (HTTP durum kodu: 204), hatalı istek (HTTP durum kodu: 400), bulunamadı (HTTP durum kodu: 404), çakışma (HTTP durum kodu: 409), iç sunucu hatası (HTTP durum kodu: 500), hizmet kullanılamıyor (HTTP durum kodu: 503), ağ geçidi zaman aşımı (HTTP durum kodu: 504)</span><span class="sxs-lookup"><span data-stu-id="2a044-185">Common substatus values include: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2a044-186">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2a044-186">Next steps</span></span>
* [<span data-ttu-id="2a044-187">Etkinlik günlüğü hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="2a044-187">Learn more about the Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="2a044-188">Azure Otomasyonu komut dosyaları (Runbook'lar) Azure uyarılar yürütme</span><span class="sxs-lookup"><span data-stu-id="2a044-188">Execute Azure Automation scripts (Runbooks) on Azure alerts</span></span>](http://go.microsoft.com/fwlink/?LinkId=627081)
* <span data-ttu-id="2a044-189">[Mantıksal uygulama Twilio aracılığıyla bir SMS gelen Azure uyarı göndermek için kullanmak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="2a044-189">[Use Logic App to send an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="2a044-190">Bu örnek için ölçüm uyarılar, ancak bir etkinlik günlüğü uyarı ile çalışması için değiştirilmesi.</span><span class="sxs-lookup"><span data-stu-id="2a044-190">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span></span>
* <span data-ttu-id="2a044-191">[Bir Azure uyarıdan Slack ileti göndermek için mantıksal uygulama kullanmak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="2a044-191">[Use Logic App to send a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="2a044-192">Bu örnek için ölçüm uyarılar, ancak bir etkinlik günlüğü uyarı ile çalışması için değiştirilmesi.</span><span class="sxs-lookup"><span data-stu-id="2a044-192">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span></span>
* <span data-ttu-id="2a044-193">[Bir Azure uyarıdan bir Azure kuyruğuna ileti göndermek için mantıksal uygulama kullanmak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="2a044-193">[Use Logic App to send a message to an Azure Queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="2a044-194">Bu örnek için ölçüm uyarılar, ancak bir etkinlik günlüğü uyarı ile çalışması için değiştirilmesi.</span><span class="sxs-lookup"><span data-stu-id="2a044-194">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span></span>
