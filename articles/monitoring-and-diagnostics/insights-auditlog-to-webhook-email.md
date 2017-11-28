---
title: "aaaCall bir Web kancası Azure etkinlik günlüğü uyarılar hakkında | Microsoft Docs"
description: "Etkinlik günlüğü olaylarını tooother Hizmetleri özel eylemler için rota. Örneğin SMS gönder, hatalar oturum veya sohbet ve mesajlaşma hizmeti üzerinden bir takım bildirin."
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
ms.openlocfilehash: 9017ff3e5165857ec7084a8f07f4123552e55f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="call-a-webhook-on-azure-activity-log-alerts"></a><span data-ttu-id="e22ab-104">Bir Web kancası Azure etkinlik günlüğü uyarılar çağırın</span><span class="sxs-lookup"><span data-stu-id="e22ab-104">Call a webhook on Azure Activity Log alerts</span></span>
<span data-ttu-id="e22ab-105">Web kancası tooroute Azure izin uyarı bildirim tooother sistemleri işlem sonrası ya da özel eylemler için.</span><span class="sxs-lookup"><span data-stu-id="e22ab-105">Webhooks allow you tooroute an Azure alert notification tooother systems for post-processing or custom actions.</span></span> <span data-ttu-id="e22ab-106">Bir uyarı tooroute üzerinde bir Web kancası kullanabilirsiniz, SMS gönder tooservices oturum hatalar, sohbet ve mesajlaşma Servisleri üzerinden takım bildirmek veya herhangi bir sayıda diğer eylemleri yapın.</span><span class="sxs-lookup"><span data-stu-id="e22ab-106">You can use a webhook on an alert tooroute it tooservices that send SMS, log bugs, notify a team via chat/messaging services, or do any number of other actions.</span></span> <span data-ttu-id="e22ab-107">Bu makalede nasıl tooset bir Web kancası toobe Azure etkinlik günlüğü uyarı ateşlenir çağrılır açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e22ab-107">This article describes how tooset a webhook toobe called when an Azure Activity Log alert fires.</span></span> <span data-ttu-id="e22ab-108">Ayrıca, hangi hello yükü hello HTTP POST tooa Web kancası gibi görünüyor gösterir.</span><span class="sxs-lookup"><span data-stu-id="e22ab-108">It also shows what hello payload for hello HTTP POST tooa webhook looks like.</span></span> <span data-ttu-id="e22ab-109">Merhaba kurulumu ve bir Azure ölçüm uyarı şeması hakkında bilgiler için [bunun yerine bu sayfaya bakın](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="e22ab-109">For information on hello setup and schema for an Azure metric alert, [see this page instead](insights-webhooks-alerts.md).</span></span> <span data-ttu-id="e22ab-110">Etkinleştirildiğinde bir etkinlik günlüğü uyarı toosend e-posta de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e22ab-110">You can also set up an Activity Log alert toosend email when activated.</span></span>

> [!NOTE]
> <span data-ttu-id="e22ab-111">Bu özellik şu anda önizlemede değil ve gelecekteki hello belirli bir noktada kaldırılacak.</span><span class="sxs-lookup"><span data-stu-id="e22ab-111">This feature is currently in preview and will be removed at some point in hello future.</span></span>
>
>

<span data-ttu-id="e22ab-112">Hello kullanarak bir etkinlik günlüğü alarm kurabilirsiniz [Azure PowerShell cmdlet'leri](insights-powershell-samples.md#create-metric-alerts), [platformlar arası CLI](insights-cli-samples.md#work-with-alerts), veya [Azure İzleyici REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span><span class="sxs-lookup"><span data-stu-id="e22ab-112">You can set up an Activity Log alert using hello [Azure PowerShell Cmdlets](insights-powershell-samples.md#create-metric-alerts), [Cross-Platform CLI](insights-cli-samples.md#work-with-alerts), or [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span></span> <span data-ttu-id="e22ab-113">Şu anda bir hello Azure portal kullanarak ayarlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="e22ab-113">Currently, you cannot set one up using hello Azure portal.</span></span>

## <a name="authenticating-hello-webhook"></a><span data-ttu-id="e22ab-114">Merhaba Web kancası kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="e22ab-114">Authenticating hello webhook</span></span>
<span data-ttu-id="e22ab-115">Merhaba Web kancası bu yöntemlerden birini kullanarak doğrulayabilir:</span><span class="sxs-lookup"><span data-stu-id="e22ab-115">hello webhook can authenticate using either of these methods:</span></span>

1. <span data-ttu-id="e22ab-116">**Belirteç tabanlı bir yetkilendirme** -URI kaydedilir belirteci Kimliğine sahip, örneğin, Web kancası hello`https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span><span class="sxs-lookup"><span data-stu-id="e22ab-116">**Token-based authorization** - hello webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span></span>
2. <span data-ttu-id="e22ab-117">**Temel yetkilendirme** -URI kaydedilir bir kullanıcı adı ve parola, örneğin, Web kancası hello`https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span><span class="sxs-lookup"><span data-stu-id="e22ab-117">**Basic authorization** - hello webhook URI is saved with a username and password, for example, `https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span></span>

## <a name="payload-schema"></a><span data-ttu-id="e22ab-118">Yükü şeması</span><span class="sxs-lookup"><span data-stu-id="e22ab-118">Payload schema</span></span>
<span data-ttu-id="e22ab-119">Merhaba POST işlemine JSON yükü ve etkinlik günlüğü tabanlı tüm uyarılar için şema aşağıdaki hello içerir.</span><span class="sxs-lookup"><span data-stu-id="e22ab-119">hello POST operation contains hello following JSON payload and schema for all Activity Log-based alerts.</span></span> <span data-ttu-id="e22ab-120">Bu şemayı bir ölçüm tabanlı uyarılar tarafından kullanılan benzer toohello ' dir.</span><span class="sxs-lookup"><span data-stu-id="e22ab-120">This schema is similar toohello one used by metric-based alerts.</span></span>

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

| <span data-ttu-id="e22ab-121">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="e22ab-121">Element Name</span></span> | <span data-ttu-id="e22ab-122">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e22ab-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e22ab-123">durum</span><span class="sxs-lookup"><span data-stu-id="e22ab-123">status</span></span> |<span data-ttu-id="e22ab-124">Ölçüm uyarılar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e22ab-124">Used for metric alerts.</span></span> <span data-ttu-id="e22ab-125">Her zaman "çok etkinlik günlüğü uyarılar için etkinleştirilmiş" ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e22ab-125">Always set too"activated" for Activity Log alerts.</span></span> |
| <span data-ttu-id="e22ab-126">bağlam</span><span class="sxs-lookup"><span data-stu-id="e22ab-126">context</span></span> |<span data-ttu-id="e22ab-127">Merhaba olay bağlamı.</span><span class="sxs-lookup"><span data-stu-id="e22ab-127">Context of hello event.</span></span> |
| <span data-ttu-id="e22ab-128">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="e22ab-128">resourceProviderName</span></span> |<span data-ttu-id="e22ab-129">Merhaba Hello kaynak sağlayıcısı kaynak etkilenmiş.</span><span class="sxs-lookup"><span data-stu-id="e22ab-129">hello resource provider of hello impacted resource.</span></span> |
| <span data-ttu-id="e22ab-130">Koşul türü</span><span class="sxs-lookup"><span data-stu-id="e22ab-130">conditionType</span></span> |<span data-ttu-id="e22ab-131">Her zaman "olayını."</span><span class="sxs-lookup"><span data-stu-id="e22ab-131">Always "Event."</span></span> |
| <span data-ttu-id="e22ab-132">ad</span><span class="sxs-lookup"><span data-stu-id="e22ab-132">name</span></span> |<span data-ttu-id="e22ab-133">Merhaba uyarı kuralının adı.</span><span class="sxs-lookup"><span data-stu-id="e22ab-133">Name of hello alert rule.</span></span> |
| <span data-ttu-id="e22ab-134">id</span><span class="sxs-lookup"><span data-stu-id="e22ab-134">id</span></span> |<span data-ttu-id="e22ab-135">Merhaba uyarı kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="e22ab-135">Resource ID of hello alert.</span></span> |
| <span data-ttu-id="e22ab-136">açıklama</span><span class="sxs-lookup"><span data-stu-id="e22ab-136">description</span></span> |<span data-ttu-id="e22ab-137">Merhaba uyarı oluşturulması sırasında uyarı açıklaması olarak ayarla.</span><span class="sxs-lookup"><span data-stu-id="e22ab-137">Alert description as set during creation of hello alert.</span></span> |
| <span data-ttu-id="e22ab-138">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="e22ab-138">subscriptionId</span></span> |<span data-ttu-id="e22ab-139">Azure abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="e22ab-139">Azure Subscription ID.</span></span> |
| <span data-ttu-id="e22ab-140">timestamp</span><span class="sxs-lookup"><span data-stu-id="e22ab-140">timestamp</span></span> |<span data-ttu-id="e22ab-141">Hangi hello olay hello hello istek işlenmeden Azure hizmeti tarafından oluşturulan saat.</span><span class="sxs-lookup"><span data-stu-id="e22ab-141">Time at which hello event was generated by hello Azure service that processed hello request.</span></span> |
| <span data-ttu-id="e22ab-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="e22ab-142">resourceId</span></span> |<span data-ttu-id="e22ab-143">Kaynak Kimliğini hello kaynak etkilenmiş.</span><span class="sxs-lookup"><span data-stu-id="e22ab-143">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="e22ab-144">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="e22ab-144">resourceGroupName</span></span> |<span data-ttu-id="e22ab-145">Kaynak hello kaynak grubunun adını hello için etkilenen</span><span class="sxs-lookup"><span data-stu-id="e22ab-145">Name of hello resource group for hello impacted resource</span></span> |
| <span data-ttu-id="e22ab-146">properties</span><span class="sxs-lookup"><span data-stu-id="e22ab-146">properties</span></span> |<span data-ttu-id="e22ab-147">Kümesi `<Key, Value>` çiftleri (yani `Dictionary<String, String>`) hello olay ayrıntılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="e22ab-147">Set of `<Key, Value>` pairs (i.e. `Dictionary<String, String>`) that includes details about hello event.</span></span> |
| <span data-ttu-id="e22ab-148">Olay</span><span class="sxs-lookup"><span data-stu-id="e22ab-148">event</span></span> |<span data-ttu-id="e22ab-149">Merhaba olayla ilgili meta verileri içeren öğe.</span><span class="sxs-lookup"><span data-stu-id="e22ab-149">Element containing metadata about hello event.</span></span> |
| <span data-ttu-id="e22ab-150">Yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="e22ab-150">authorization</span></span> |<span data-ttu-id="e22ab-151">Merhaba olay Hello RBAC özellikleri.</span><span class="sxs-lookup"><span data-stu-id="e22ab-151">hello RBAC properties of hello event.</span></span> <span data-ttu-id="e22ab-152">Bunlar genellikle hello "eylem" ve "rol" hello "scope." içerir</span><span class="sxs-lookup"><span data-stu-id="e22ab-152">These usually include hello “action”, “role” and hello “scope.”</span></span> |
| <span data-ttu-id="e22ab-153">category</span><span class="sxs-lookup"><span data-stu-id="e22ab-153">category</span></span> |<span data-ttu-id="e22ab-154">Merhaba olay kategorisi.</span><span class="sxs-lookup"><span data-stu-id="e22ab-154">Category of hello event.</span></span> <span data-ttu-id="e22ab-155">Desteklenen değerler: yönetici, uyarı, güvenlik, ServiceHealth, öneri.</span><span class="sxs-lookup"><span data-stu-id="e22ab-155">Supported values include: Administrative, Alert, Security, ServiceHealth, Recommendation.</span></span> |
| <span data-ttu-id="e22ab-156">Arayan</span><span class="sxs-lookup"><span data-stu-id="e22ab-156">caller</span></span> |<span data-ttu-id="e22ab-157">Merhaba işlemi, UPN Talebi veya kullanılabilirliğine göre SPN talep gerçekleştiren hello kullanıcının e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="e22ab-157">Email address of hello user who performed hello operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="e22ab-158">Belirli sistem çağrıları için null olabilir.</span><span class="sxs-lookup"><span data-stu-id="e22ab-158">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="e22ab-159">correlationId</span><span class="sxs-lookup"><span data-stu-id="e22ab-159">correlationId</span></span> |<span data-ttu-id="e22ab-160">Genellikle bir GUID dize biçiminde.</span><span class="sxs-lookup"><span data-stu-id="e22ab-160">Usually a GUID in string format.</span></span> <span data-ttu-id="e22ab-161">Correlationıd değeri olaylarla ait toohello aynı büyük eylemi ve genellikle bir correlationıd değeri paylaşın.</span><span class="sxs-lookup"><span data-stu-id="e22ab-161">Events with correlationId belong toohello same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="e22ab-162">eventDescription</span><span class="sxs-lookup"><span data-stu-id="e22ab-162">eventDescription</span></span> |<span data-ttu-id="e22ab-163">Merhaba Olay açıklaması statik metin.</span><span class="sxs-lookup"><span data-stu-id="e22ab-163">Static text description of hello event.</span></span> |
| <span data-ttu-id="e22ab-164">eventDataId</span><span class="sxs-lookup"><span data-stu-id="e22ab-164">eventDataId</span></span> |<span data-ttu-id="e22ab-165">Merhaba olay için benzersiz tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="e22ab-165">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="e22ab-166">EventSource</span><span class="sxs-lookup"><span data-stu-id="e22ab-166">eventSource</span></span> |<span data-ttu-id="e22ab-167">Hello Azure hizmetine veya altyapı oluşturulan hello olayın adı.</span><span class="sxs-lookup"><span data-stu-id="e22ab-167">Name of hello Azure service or infrastructure that generated hello event.</span></span> |
| <span data-ttu-id="e22ab-168">httpRequest</span><span class="sxs-lookup"><span data-stu-id="e22ab-168">httpRequest</span></span> |<span data-ttu-id="e22ab-169">Genellikle hello "clientRequestId", "clientIpAddress" ve "yöntem" içerir (örneğin PUT HTTP yöntemi).</span><span class="sxs-lookup"><span data-stu-id="e22ab-169">Usually includes hello “clientRequestId”, “clientIpAddress” and “method” (HTTP method e.g. PUT).</span></span> |
| <span data-ttu-id="e22ab-170">düzeyi</span><span class="sxs-lookup"><span data-stu-id="e22ab-170">level</span></span> |<span data-ttu-id="e22ab-171">Değerleri aşağıdaki hello birini: "Kritik", "Error"Uyarı",", "Bilgi" ve "Ayrıntılı."</span><span class="sxs-lookup"><span data-stu-id="e22ab-171">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose.”</span></span> |
| <span data-ttu-id="e22ab-172">Operationıd</span><span class="sxs-lookup"><span data-stu-id="e22ab-172">operationId</span></span> |<span data-ttu-id="e22ab-173">Toosingle işlemi karşılık gelen hello olaylar arasında paylaşılan genellikle bir GUID.</span><span class="sxs-lookup"><span data-stu-id="e22ab-173">Usually a GUID shared among hello events corresponding toosingle operation.</span></span> |
| <span data-ttu-id="e22ab-174">operationName</span><span class="sxs-lookup"><span data-stu-id="e22ab-174">operationName</span></span> |<span data-ttu-id="e22ab-175">Merhaba işlemin adı.</span><span class="sxs-lookup"><span data-stu-id="e22ab-175">Name of hello operation.</span></span> |
| <span data-ttu-id="e22ab-176">properties</span><span class="sxs-lookup"><span data-stu-id="e22ab-176">properties</span></span> |<span data-ttu-id="e22ab-177">Merhaba olay özellikleri.</span><span class="sxs-lookup"><span data-stu-id="e22ab-177">Properties of hello event.</span></span> |
| <span data-ttu-id="e22ab-178">durum</span><span class="sxs-lookup"><span data-stu-id="e22ab-178">status</span></span> |<span data-ttu-id="e22ab-179">Dize.</span><span class="sxs-lookup"><span data-stu-id="e22ab-179">String.</span></span> <span data-ttu-id="e22ab-180">Merhaba işlem durumu.</span><span class="sxs-lookup"><span data-stu-id="e22ab-180">Status of hello operation.</span></span> <span data-ttu-id="e22ab-181">Genel değerler şunlardır: "Başlatıldı", "Sürüyor", "Başarılı", "Başarısız", "Active", "Çözülmüş".</span><span class="sxs-lookup"><span data-stu-id="e22ab-181">Common values include: "Started", "In Progress", "Succeeded", "Failed", "Active", "Resolved".</span></span> |
| <span data-ttu-id="e22ab-182">alt durum</span><span class="sxs-lookup"><span data-stu-id="e22ab-182">subStatus</span></span> |<span data-ttu-id="e22ab-183">Genellikle hello karşılık gelen REST çağrısı hello HTTP durum kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="e22ab-183">Usually includes hello HTTP status code of hello corresponding REST call.</span></span> <span data-ttu-id="e22ab-184">Ayrıca, bir alt durum açıklayan diğer dizeleri de içerebilir.</span><span class="sxs-lookup"><span data-stu-id="e22ab-184">It might also include other strings describing a substatus.</span></span> <span data-ttu-id="e22ab-185">Ortak alt durum değerleri şunları içerir: Tamam (HTTP durum kodu: 200), oluşturulan (HTTP durum kodu: 201), kabul edilen (HTTP durum kodu: 202), Hayır içeriği (HTTP durum kodu: 204), hatalı istek (HTTP durum kodu: 400), bulunamadı (HTTP durum kodu: 404), çakışma (HTTP durum kodu: 409), iç sunucu hatası (HTTP durum kodu: 500), hizmet kullanılamıyor (HTTP durum kodu: 503), ağ geçidi zaman aşımı (HTTP durum kodu: 504)</span><span class="sxs-lookup"><span data-stu-id="e22ab-185">Common substatus values include: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e22ab-186">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e22ab-186">Next steps</span></span>
* [<span data-ttu-id="e22ab-187">Merhaba etkinlik günlüğü hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="e22ab-187">Learn more about hello Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="e22ab-188">Azure Otomasyonu komut dosyaları (Runbook'lar) Azure uyarılar yürütme</span><span class="sxs-lookup"><span data-stu-id="e22ab-188">Execute Azure Automation scripts (Runbooks) on Azure alerts</span></span>](http://go.microsoft.com/fwlink/?LinkId=627081)
* <span data-ttu-id="e22ab-189">[Bir Azure uyarıdan mantıksal uygulama toosend Twilio aracılığıyla bir SMS kullanmak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="e22ab-189">[Use Logic App toosend an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="e22ab-190">Bu örnek için ölçüm uyarılar, ancak bir etkinlik günlüğü uyarı ile değiştirilmiş toowork olabilir.</span><span class="sxs-lookup"><span data-stu-id="e22ab-190">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
* <span data-ttu-id="e22ab-191">[Mantıksal uygulama toosend Azure uyarı Slack iletiden kullanmak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="e22ab-191">[Use Logic App toosend a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="e22ab-192">Bu örnek için ölçüm uyarılar, ancak bir etkinlik günlüğü uyarı ile değiştirilmiş toowork olabilir.</span><span class="sxs-lookup"><span data-stu-id="e22ab-192">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
* <span data-ttu-id="e22ab-193">[Mantıksal uygulama toosend Azure bir uyarıdan ileti tooan Azure kuyruk kullanmak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="e22ab-193">[Use Logic App toosend a message tooan Azure Queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="e22ab-194">Bu örnek için ölçüm uyarılar, ancak bir etkinlik günlüğü uyarı ile değiştirilmiş toowork olabilir.</span><span class="sxs-lookup"><span data-stu-id="e22ab-194">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
