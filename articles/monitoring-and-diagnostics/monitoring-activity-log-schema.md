---
title: "Etkinlik günlüğü olay şeması aaaAzure | Microsoft Docs"
description: "Etkinlik günlüğü hello yayılan veriler için Hello olay şeması anlama"
author: johnkemnetz
manager: robb
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: johnkem
ms.openlocfilehash: dfece949a20a4d9b4e8a4d488c1c34842d87d586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-activity-log-event-schema"></a><span data-ttu-id="323ad-103">Azure etkinlik günlüğü olay şeması</span><span class="sxs-lookup"><span data-stu-id="323ad-103">Azure Activity Log event schema</span></span>
<span data-ttu-id="323ad-104">Merhaba **Azure etkinlik günlüğü** Azure'da oluşan herhangi bir abonelik düzeyi olayı bir anlayış sağlar günlüktür.</span><span class="sxs-lookup"><span data-stu-id="323ad-104">hello **Azure Activity Log** is a log that provides insight into any subscription-level events that have occurred in Azure.</span></span> <span data-ttu-id="323ad-105">Bu makalede hello olay şema veri kategorisi başına açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="323ad-105">This article describes hello event schema per category of data.</span></span>

## <a name="administrative"></a><span data-ttu-id="323ad-106">Yönetim</span><span class="sxs-lookup"><span data-stu-id="323ad-106">Administrative</span></span>
<span data-ttu-id="323ad-107">Bu kategorideki tüm hello kayıt içeren oluşturma, güncelleştirme, silme ve eylem işlemlerine Resource Manager aracılığıyla gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="323ad-107">This category contains hello record of all create, update, delete, and action operations performed through Resource Manager.</span></span> <span data-ttu-id="323ad-108">Bu kategorideki görür olay türleri dahil hello örnekleri "sanal makine oluşturma" ve "ağ güvenlik grubu bir kullanıcı tarafından gerçekleştirilen her eylem delete" veya Kaynak Yöneticisi'ni kullanarak uygulama belirli bir kaynak türü üzerinde bir işlemi olarak modellenir.</span><span class="sxs-lookup"><span data-stu-id="323ad-108">Examples of hello types of events you would see in this category include "create virtual machine" and "delete network security group" Every action taken by a user or application using Resource Manager is modeled as an operation on a particular resource type.</span></span> <span data-ttu-id="323ad-109">Merhaba işlem türü ise yazma, silme veya eylem hello kayıtlarını hello başlangıç ve başarı veya işlemi hello yönetim kategorisinde kaydedilir başarısız.</span><span class="sxs-lookup"><span data-stu-id="323ad-109">If hello operation type is Write, Delete, or Action, hello records of both hello start and success or fail of that operation are recorded in hello Administrative category.</span></span> <span data-ttu-id="323ad-110">Merhaba yönetim kategorisi, ayrıca bir abonelikte herhangi bir değişiklik toorole tabanlı erişim denetimi içerir.</span><span class="sxs-lookup"><span data-stu-id="323ad-110">hello Administrative category also includes any changes toorole-based access control in a subscription.</span></span>

### <a name="sample-event"></a><span data-ttu-id="323ad-111">Örnek olayı</span><span class="sxs-lookup"><span data-stu-id="323ad-111">Sample event</span></span>
```json
{
  "authorization": {
    "action": "microsoft.support/supporttickets/write",
    "role": "Subscription Admin",
    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841"
  },
  "caller": "admin@contoso.com",
  "channels": "Operation",
  "claims": {
    "aud": "https://management.core.windows.net/",
    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
    "iat": "1421876371",
    "nbf": "1421876371",
    "exp": "1421880271",
    "ver": "1.0",
    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
    "puid": "20030000801A118C",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
    "name": "John Smith",
    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
    "appidacr": "2",
    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
    "http://schemas.microsoft.com/claims/authnclassreference": "1"
  },
  "correlationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "description": "",
  "eventDataId": "44ade6b4-3813-45e6-ae27-7420a95fa2f8",
  "eventName": {
    "value": "EndRequest",
    "localizedValue": "End request"
  },
  "httpRequest": {
    "clientRequestId": "27003b25-91d3-418f-8eb1-29e537dcb249",
    "clientIpAddress": "192.168.35.115",
    "method": "PUT"
  },
  "id": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841/events/44ade6b4-3813-45e6-ae27-7420a95fa2f8/ticks/635574752669792776",
  "level": "Informational",
  "resourceGroupName": "MSSupportGroup",
  "resourceProviderName": {
    "value": "microsoft.support",
    "localizedValue": "microsoft.support"
  },
  "resourceUri": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
  "operationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "operationName": {
    "value": "microsoft.support/supporttickets/write",
    "localizedValue": "microsoft.support/supporttickets/write"
  },
  "properties": {
    "statusCode": "Created"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": "Created",
    "localizedValue": "Created (HTTP Status Code: 201)"
  },
  "eventTimestamp": "2015-01-21T22:14:26.9792776Z",
  "submissionTimestamp": "2015-01-21T22:14:39.9936304Z",
  "subscriptionId": "s1"
}
```

### <a name="property-descriptions"></a><span data-ttu-id="323ad-112">Özellik açıklamaları</span><span class="sxs-lookup"><span data-stu-id="323ad-112">Property descriptions</span></span>
| <span data-ttu-id="323ad-113">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="323ad-113">Element Name</span></span> | <span data-ttu-id="323ad-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="323ad-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="323ad-115">Yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="323ad-115">authorization</span></span> |<span data-ttu-id="323ad-116">BLOB hello olay RBAC özelliklerinin.</span><span class="sxs-lookup"><span data-stu-id="323ad-116">Blob of RBAC properties of hello event.</span></span> <span data-ttu-id="323ad-117">Genellikle hello "eylem", "rol" ve "scope" özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="323ad-117">Usually includes hello “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="323ad-118">Arayan</span><span class="sxs-lookup"><span data-stu-id="323ad-118">caller</span></span> |<span data-ttu-id="323ad-119">Merhaba işlemi, UPN Talebi veya kullanılabilirliğine göre SPN talep yürüttü hello kullanıcının e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="323ad-119">Email address of hello user who has performed hello operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="323ad-120">Kanalları</span><span class="sxs-lookup"><span data-stu-id="323ad-120">channels</span></span> |<span data-ttu-id="323ad-121">Değerleri aşağıdaki hello birini: "Yönetici", "İşlem"</span><span class="sxs-lookup"><span data-stu-id="323ad-121">One of hello following values: “Admin”, “Operation”</span></span> |
| <span data-ttu-id="323ad-122">Talepleri</span><span class="sxs-lookup"><span data-stu-id="323ad-122">claims</span></span> |<span data-ttu-id="323ad-123">Merhaba JWT belirteci Kaynak Yöneticisi'nde bu işlem Active Directory tooauthenticate hello kullanıcı veya uygulama tooperform tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="323ad-123">hello JWT token used by Active Directory tooauthenticate hello user or application tooperform this operation in resource manager.</span></span> |
| <span data-ttu-id="323ad-124">correlationId</span><span class="sxs-lookup"><span data-stu-id="323ad-124">correlationId</span></span> |<span data-ttu-id="323ad-125">Genellikle bir GUID hello dize biçiminde.</span><span class="sxs-lookup"><span data-stu-id="323ad-125">Usually a GUID in hello string format.</span></span> <span data-ttu-id="323ad-126">Bir correlationıd değeri paylaşan olayları ait toohello aynı uber eylemi.</span><span class="sxs-lookup"><span data-stu-id="323ad-126">Events that share a correlationId belong toohello same uber action.</span></span> |
| <span data-ttu-id="323ad-127">Açıklama</span><span class="sxs-lookup"><span data-stu-id="323ad-127">description</span></span> |<span data-ttu-id="323ad-128">Olay açıklaması statik metin.</span><span class="sxs-lookup"><span data-stu-id="323ad-128">Static text description of an event.</span></span> |
| <span data-ttu-id="323ad-129">eventDataId</span><span class="sxs-lookup"><span data-stu-id="323ad-129">eventDataId</span></span> |<span data-ttu-id="323ad-130">Bir olay benzersiz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="323ad-130">Unique identifier of an event.</span></span> |
| <span data-ttu-id="323ad-131">httpRequest</span><span class="sxs-lookup"><span data-stu-id="323ad-131">httpRequest</span></span> |<span data-ttu-id="323ad-132">BLOB açıklayan hello Http isteği.</span><span class="sxs-lookup"><span data-stu-id="323ad-132">Blob describing hello Http Request.</span></span> <span data-ttu-id="323ad-133">Merhaba "clientRequestId", "clientIpAddress" ve "yöntem" (HTTP yöntemi. genellikle içerir</span><span class="sxs-lookup"><span data-stu-id="323ad-133">Usually includes hello “clientRequestId”, “clientIpAddress” and “method” (HTTP method.</span></span> <span data-ttu-id="323ad-134">For example, PUT).</span><span class="sxs-lookup"><span data-stu-id="323ad-134">For example, PUT).</span></span> |
| <span data-ttu-id="323ad-135">düzeyi</span><span class="sxs-lookup"><span data-stu-id="323ad-135">level</span></span> |<span data-ttu-id="323ad-136">Merhaba olay düzeyi.</span><span class="sxs-lookup"><span data-stu-id="323ad-136">Level of hello event.</span></span> <span data-ttu-id="323ad-137">Değerleri aşağıdaki hello birini: "Kritik", "Error"Uyarı",", "Bilgi" ve "Ayrıntılı"</span><span class="sxs-lookup"><span data-stu-id="323ad-137">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="323ad-138">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="323ad-138">resourceGroupName</span></span> |<span data-ttu-id="323ad-139">Merhaba hello kaynak grubunun adı, kaynak etkilenmiş.</span><span class="sxs-lookup"><span data-stu-id="323ad-139">Name of hello resource group for hello impacted resource.</span></span> |
| <span data-ttu-id="323ad-140">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="323ad-140">resourceProviderName</span></span> |<span data-ttu-id="323ad-141">Kaynak hello kaynak sağlayıcısının adını hello için etkilenen</span><span class="sxs-lookup"><span data-stu-id="323ad-141">Name of hello resource provider for hello impacted resource</span></span> |
| <span data-ttu-id="323ad-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="323ad-142">resourceId</span></span> |<span data-ttu-id="323ad-143">Kaynak kimliğini hello kaynak etkilenmiş.</span><span class="sxs-lookup"><span data-stu-id="323ad-143">Resource id of hello impacted resource.</span></span> |
| <span data-ttu-id="323ad-144">Operationıd</span><span class="sxs-lookup"><span data-stu-id="323ad-144">operationId</span></span> |<span data-ttu-id="323ad-145">Tooa tek bir işlem karşılık gelen hello olayları arasında paylaşılan bir GUID.</span><span class="sxs-lookup"><span data-stu-id="323ad-145">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="323ad-146">operationName</span><span class="sxs-lookup"><span data-stu-id="323ad-146">operationName</span></span> |<span data-ttu-id="323ad-147">Merhaba işlemin adı.</span><span class="sxs-lookup"><span data-stu-id="323ad-147">Name of hello operation.</span></span> |
| <span data-ttu-id="323ad-148">properties</span><span class="sxs-lookup"><span data-stu-id="323ad-148">properties</span></span> |<span data-ttu-id="323ad-149">Kümesi `<Key, Value>` hello hello olay ayrıntılarını açıklayan çiftleri (diğer bir deyişle, bir sözlük).</span><span class="sxs-lookup"><span data-stu-id="323ad-149">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="323ad-150">durum</span><span class="sxs-lookup"><span data-stu-id="323ad-150">status</span></span> |<span data-ttu-id="323ad-151">Merhaba hello işlemi durumunu açıklayan dize.</span><span class="sxs-lookup"><span data-stu-id="323ad-151">String describing hello status of hello operation.</span></span> <span data-ttu-id="323ad-152">Bazı genel değerler şunlardır:, ilerleme, başarılı, başarısız, etkin, çözümlenmiş başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="323ad-152">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="323ad-153">alt durum</span><span class="sxs-lookup"><span data-stu-id="323ad-153">subStatus</span></span> |<span data-ttu-id="323ad-154">Genellikle hello REST çağrısı karşılık gelen HTTP durum kodunu Merhaba, ancak bu ortak değerleri gibi bir alt durum açıklayan diğer dizeleri de içerir: Tamam (HTTP durum kodu: 200), oluşturulan (HTTP durum kodu: 201), kabul edilen (HTTP durum kodu: 202), içerik yok (HTTP Durum kodu: 204), hatalı istek (HTTP durum kodu: 400), bulunamadı (HTTP durum kodu: 404), çakışma (HTTP durum kodu: 409), iç sunucu hatası (HTTP durum kodu: 500), hizmet kullanılamıyor (HTTP durum kodu: 503), ağ geçidi zaman aşımı (HTTP durum kodu: 504).</span><span class="sxs-lookup"><span data-stu-id="323ad-154">Usually hello HTTP status code of hello corresponding REST call, but can also include other strings describing a substatus, such as these common values: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504).</span></span> |
| <span data-ttu-id="323ad-155">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="323ad-155">eventTimestamp</span></span> |<span data-ttu-id="323ad-156">Merhaba olay hello Azure hizmetini işleme hello tarafından oluşturulan zaman damgası karşılık gelen hello olay isteği.</span><span class="sxs-lookup"><span data-stu-id="323ad-156">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="323ad-157">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="323ad-157">submissionTimestamp</span></span> |<span data-ttu-id="323ad-158">Merhaba olay sorgulama için kullanılabilir duruma zaman damgası.</span><span class="sxs-lookup"><span data-stu-id="323ad-158">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="323ad-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="323ad-159">subscriptionId</span></span> |<span data-ttu-id="323ad-160">Azure abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="323ad-160">Azure Subscription Id.</span></span> |

## <a name="service-health"></a><span data-ttu-id="323ad-161">Hizmet durumu</span><span class="sxs-lookup"><span data-stu-id="323ad-161">Service health</span></span>
<span data-ttu-id="323ad-162">Bu kategori, Azure'da oluşan herhangi bir hizmet durumu olay hello kaydını içerir.</span><span class="sxs-lookup"><span data-stu-id="323ad-162">This category contains hello record of any service health incidents that have occurred in Azure.</span></span> <span data-ttu-id="323ad-163">Bu kategorideki görür olay hello türü "SQL Azure Doğu ABD kesinti yaşanıyor." örneğidir</span><span class="sxs-lookup"><span data-stu-id="323ad-163">An example of hello type of event you would see in this category is "SQL Azure in East US is experiencing downtime."</span></span> <span data-ttu-id="323ad-164">Hizmet sistem durumu olayları beş çeşit olarak gelir: eylem gerekli, Destekli kurtarma, olay, bakım, bilgi veya güvenlik ve hello olay tarafından etkilenen hello Abonelikteki bir kaynağınız varsa yalnızca görünür.</span><span class="sxs-lookup"><span data-stu-id="323ad-164">Service health events come in five varieties: Action Required, Assisted Recovery, Incident, Maintenance, Information, or Security, and only appear if you have a resource in hello subscription that would be impacted by hello event.</span></span>

### <a name="sample-event"></a><span data-ttu-id="323ad-165">Örnek olayı</span><span class="sxs-lookup"><span data-stu-id="323ad-165">Sample event</span></span>
```json
{
  "channels": "Admin",
  "correlationId": "c550176b-8f52-4380-bdc5-36c1b59d3a44",
  "description": "Active: Network Infrastructure - UK South",
  "eventDataId": "c5bc4514-6642-2be3-453e-c6a67841b073",
  "eventName": {
      "value": null
  },
  "category": {
      "value": "ServiceHealth",
      "localizedValue": "Service Health"
  },
  "eventTimestamp": "2017-07-20T23:30:14.8022297Z",
  "id": "/subscriptions/mySubscriptionID/events/c5bc4514-6642-2be3-453e-c6a67841b073/ticks/636361902148022297",
  "level": "Warning",
  "operationName": {
      "value": "Microsoft.ServiceHealth/incident/action",
      "localizedValue": "Microsoft.ServiceHealth/incident/action"
  },
  "resourceProviderName": {
      "value": null
  },
  "resourceType": {
      "value": null,
      "localizedValue": ""
  },
  "resourceId": "/subscriptions/mySubscriptionID",
  "status": {
      "value": "Active",
      "localizedValue": "Active"
  },
  "subStatus": {
      "value": null
  },
  "submissionTimestamp": "2017-07-20T23:30:34.7431946Z",
  "subscriptionId": "mySubscriptionID",
  "properties": {
    "title": "Network Infrastructure - UK South",
    "service": "Service Fabric",
    "region": "UK South",
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```

### <a name="property-descriptions"></a><span data-ttu-id="323ad-166">Özellik açıklamaları</span><span class="sxs-lookup"><span data-stu-id="323ad-166">Property descriptions</span></span>
<span data-ttu-id="323ad-167">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="323ad-167">Element Name</span></span> | <span data-ttu-id="323ad-168">Açıklama</span><span class="sxs-lookup"><span data-stu-id="323ad-168">Description</span></span>
-------- | -----------
<span data-ttu-id="323ad-169">Kanalları</span><span class="sxs-lookup"><span data-stu-id="323ad-169">channels</span></span> | <span data-ttu-id="323ad-170">Değerleri aşağıdaki hello biridir: "Yönetici", "İşlem"</span><span class="sxs-lookup"><span data-stu-id="323ad-170">Is one of hello following values: “Admin”, “Operation”</span></span>
<span data-ttu-id="323ad-171">correlationId</span><span class="sxs-lookup"><span data-stu-id="323ad-171">correlationId</span></span> | <span data-ttu-id="323ad-172">Genellikle bir hello dize biçimindeki GUID'dir.</span><span class="sxs-lookup"><span data-stu-id="323ad-172">Is usually a GUID in hello string format.</span></span> <span data-ttu-id="323ad-173">Olaylar, ile ait aynı uber eylemi genellikle paylaşmak toohello hello aynı correlationıd değeri.</span><span class="sxs-lookup"><span data-stu-id="323ad-173">Events with that belong toohello same uber action usually share hello same correlationId.</span></span>
<span data-ttu-id="323ad-174">Açıklama</span><span class="sxs-lookup"><span data-stu-id="323ad-174">description</span></span> | <span data-ttu-id="323ad-175">Merhaba Olay açıklaması.</span><span class="sxs-lookup"><span data-stu-id="323ad-175">Description of hello event.</span></span>
<span data-ttu-id="323ad-176">eventDataId</span><span class="sxs-lookup"><span data-stu-id="323ad-176">eventDataId</span></span> | <span data-ttu-id="323ad-177">bir olayın Hello benzersiz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="323ad-177">hello unique identifier of an event.</span></span>
<span data-ttu-id="323ad-178">EventName</span><span class="sxs-lookup"><span data-stu-id="323ad-178">eventName</span></span> | <span data-ttu-id="323ad-179">Merhaba olay Hello başlığı.</span><span class="sxs-lookup"><span data-stu-id="323ad-179">hello title of hello event.</span></span>
<span data-ttu-id="323ad-180">düzeyi</span><span class="sxs-lookup"><span data-stu-id="323ad-180">level</span></span> | <span data-ttu-id="323ad-181">Merhaba olay düzeyi.</span><span class="sxs-lookup"><span data-stu-id="323ad-181">Level of hello event.</span></span> <span data-ttu-id="323ad-182">Değerleri aşağıdaki hello birini: "Kritik", "Error"Uyarı",", "Bilgi" ve "Ayrıntılı"</span><span class="sxs-lookup"><span data-stu-id="323ad-182">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span>
<span data-ttu-id="323ad-183">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="323ad-183">resourceProviderName</span></span> | <span data-ttu-id="323ad-184">Merhaba kaynak sağlayıcısının adını hello için kaynak etkilenmiş.</span><span class="sxs-lookup"><span data-stu-id="323ad-184">Name of hello resource provider for hello impacted resource.</span></span> <span data-ttu-id="323ad-185">Bilinmiyor, bu boş olacaktır.</span><span class="sxs-lookup"><span data-stu-id="323ad-185">If not known, this will be null.</span></span>
<span data-ttu-id="323ad-186">Kaynak türü</span><span class="sxs-lookup"><span data-stu-id="323ad-186">resourceType</span></span>| <span data-ttu-id="323ad-187">Merhaba, kaynak Hello türü kaynak etkilenmiş.</span><span class="sxs-lookup"><span data-stu-id="323ad-187">hello type of resource of hello impacted resource.</span></span> <span data-ttu-id="323ad-188">Bilinmiyor, bu boş olacaktır.</span><span class="sxs-lookup"><span data-stu-id="323ad-188">If not known, this will be null.</span></span>
<span data-ttu-id="323ad-189">alt durum</span><span class="sxs-lookup"><span data-stu-id="323ad-189">subStatus</span></span> | <span data-ttu-id="323ad-190">Genellikle hizmet sistem durumu olayları için null.</span><span class="sxs-lookup"><span data-stu-id="323ad-190">Usually null for Service Health events.</span></span>
<span data-ttu-id="323ad-191">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="323ad-191">eventTimestamp</span></span> | <span data-ttu-id="323ad-192">Merhaba günlük olay oluşturuldu ve toohello etkinlik günlüğü gönderilen zaman damgası.</span><span class="sxs-lookup"><span data-stu-id="323ad-192">Timestamp when hello log event was generated and submitted toohello Activity Log.</span></span>
<span data-ttu-id="323ad-193">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="323ad-193">submissionTimestamp</span></span> |   <span data-ttu-id="323ad-194">Merhaba olay hello etkinlik günlüğü kullanılabilen zaman damgası.</span><span class="sxs-lookup"><span data-stu-id="323ad-194">Timestamp when hello event became available in hello Activity Log.</span></span>
<span data-ttu-id="323ad-195">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="323ad-195">subscriptionId</span></span> | <span data-ttu-id="323ad-196">Bu olayın günlüğe yazıldığı Azure aboneliği hello.</span><span class="sxs-lookup"><span data-stu-id="323ad-196">hello Azure subscription in which this event was logged.</span></span>
<span data-ttu-id="323ad-197">durum</span><span class="sxs-lookup"><span data-stu-id="323ad-197">status</span></span> | <span data-ttu-id="323ad-198">Merhaba hello işlemi durumunu açıklayan dize.</span><span class="sxs-lookup"><span data-stu-id="323ad-198">String describing hello status of hello operation.</span></span> <span data-ttu-id="323ad-199">Bazı genel değerler şunlardır: etkin, çözüldü.</span><span class="sxs-lookup"><span data-stu-id="323ad-199">Some common values are: Active, Resolved.</span></span>
<span data-ttu-id="323ad-200">operationName</span><span class="sxs-lookup"><span data-stu-id="323ad-200">operationName</span></span> | <span data-ttu-id="323ad-201">Merhaba işlemin adı.</span><span class="sxs-lookup"><span data-stu-id="323ad-201">Name of hello operation.</span></span> <span data-ttu-id="323ad-202">Genellikle Microsoft.ServiceHealth/incident/action.</span><span class="sxs-lookup"><span data-stu-id="323ad-202">Usually Microsoft.ServiceHealth/incident/action.</span></span>
<span data-ttu-id="323ad-203">category</span><span class="sxs-lookup"><span data-stu-id="323ad-203">category</span></span> | <span data-ttu-id="323ad-204">"ServiceHealth"</span><span class="sxs-lookup"><span data-stu-id="323ad-204">"ServiceHealth"</span></span>
<span data-ttu-id="323ad-205">resourceId</span><span class="sxs-lookup"><span data-stu-id="323ad-205">resourceId</span></span> | <span data-ttu-id="323ad-206">Kaynak kimliğini hello kaynağı biliniyorsa etkilenmiş.</span><span class="sxs-lookup"><span data-stu-id="323ad-206">Resource id of hello impacted resource, if known.</span></span> <span data-ttu-id="323ad-207">Abonelik kimliği aksi sağlanır.</span><span class="sxs-lookup"><span data-stu-id="323ad-207">Subscription ID is provided otherwise.</span></span>
<span data-ttu-id="323ad-208">Properties.Title</span><span class="sxs-lookup"><span data-stu-id="323ad-208">Properties.title</span></span> | <span data-ttu-id="323ad-209">Bu iletişim için yerelleştirilmiş hello başlığı.</span><span class="sxs-lookup"><span data-stu-id="323ad-209">hello localized title for this communication.</span></span> <span data-ttu-id="323ad-210">İngilizce hello varsayılan dildir.</span><span class="sxs-lookup"><span data-stu-id="323ad-210">English is hello default language.</span></span>
<span data-ttu-id="323ad-211">Properties.Communication</span><span class="sxs-lookup"><span data-stu-id="323ad-211">Properties.communication</span></span> | <span data-ttu-id="323ad-212">Merhaba, HTML biçimlendirmesi ile Merhaba iletişim ayrıntılarını yerelleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="323ad-212">hello localized details of hello communication with HTML markup.</span></span> <span data-ttu-id="323ad-213">İngilizce hello varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="323ad-213">English is hello default.</span></span>
<span data-ttu-id="323ad-214">Properties.incidentType</span><span class="sxs-lookup"><span data-stu-id="323ad-214">Properties.incidentType</span></span> | <span data-ttu-id="323ad-215">Olası değerler: AssistedRecovery, ActionRequired, bilgi, olay, bakım, güvenlik</span><span class="sxs-lookup"><span data-stu-id="323ad-215">Possible values: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security</span></span>
<span data-ttu-id="323ad-216">Properties.trackingId</span><span class="sxs-lookup"><span data-stu-id="323ad-216">Properties.trackingId</span></span> | <span data-ttu-id="323ad-217">Bu olay ile ilişkilendirilmiş hello olay tanımlar.</span><span class="sxs-lookup"><span data-stu-id="323ad-217">Identifies hello incident this event is associated with.</span></span> <span data-ttu-id="323ad-218">Bu toocorrelate hello olayları ilgili tooan olayı kullanın.</span><span class="sxs-lookup"><span data-stu-id="323ad-218">Use this toocorrelate hello events related tooan incident.</span></span>
<span data-ttu-id="323ad-219">Properties.impactedServices</span><span class="sxs-lookup"><span data-stu-id="323ad-219">Properties.impactedServices</span></span> | <span data-ttu-id="323ad-220">Merhaba Hizmetleri ve hello olaydan etkilenen bölgeler açıklar bir kaçış karakterli JSON blobu.</span><span class="sxs-lookup"><span data-stu-id="323ad-220">An escaped JSON blob which describes hello services and regions that are impacted by hello incident.</span></span> <span data-ttu-id="323ad-221">Her biri bir ServiceName ve her biri bir RegionName sahip ImpactedRegions listesini sahip hizmetlerin listesini.</span><span class="sxs-lookup"><span data-stu-id="323ad-221">A list of Services, each of which has a ServiceName and a list of ImpactedRegions, each of which has a RegionName.</span></span>
<span data-ttu-id="323ad-222">Properties.defaultLanguageTitle</span><span class="sxs-lookup"><span data-stu-id="323ad-222">Properties.defaultLanguageTitle</span></span> | <span data-ttu-id="323ad-223">İngilizce Hello iletişimi</span><span class="sxs-lookup"><span data-stu-id="323ad-223">hello communication in English</span></span>
<span data-ttu-id="323ad-224">Properties.defaultLanguageContent</span><span class="sxs-lookup"><span data-stu-id="323ad-224">Properties.defaultLanguageContent</span></span> | <span data-ttu-id="323ad-225">html biçimlendirmesi veya düz metin olarak İngilizce Hello iletişimi</span><span class="sxs-lookup"><span data-stu-id="323ad-225">hello communication in English as either html markup or plain text</span></span>
<span data-ttu-id="323ad-226">Properties.Stage</span><span class="sxs-lookup"><span data-stu-id="323ad-226">Properties.stage</span></span> | <span data-ttu-id="323ad-227">AssistedRecovery, ActionRequired, bilgi, olay, güvenlik için olası değerler: etkin, olan çözümlendi.</span><span class="sxs-lookup"><span data-stu-id="323ad-227">Possible values for AssistedRecovery, ActionRequired, Information, Incident, Security: are Active, Resolved.</span></span> <span data-ttu-id="323ad-228">Bakım için oldukları: etkin, planlanmış, devam ediyor, iptal edildi, Rescheduled, çözümlenmiş, tamamlandı</span><span class="sxs-lookup"><span data-stu-id="323ad-228">For Maintenance they are: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete</span></span>
<span data-ttu-id="323ad-229">Properties.communicationId</span><span class="sxs-lookup"><span data-stu-id="323ad-229">Properties.communicationId</span></span> | <span data-ttu-id="323ad-230">Bu olay Hello iletişimi ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="323ad-230">hello communication this event is associated.</span></span>

## <a name="alert"></a><span data-ttu-id="323ad-231">Uyarı</span><span class="sxs-lookup"><span data-stu-id="323ad-231">Alert</span></span>
<span data-ttu-id="323ad-232">Bu kategorideki tüm etkinleştirmeleri Azure uyarıların hello kaydını içerir.</span><span class="sxs-lookup"><span data-stu-id="323ad-232">This category contains hello record of all activations of Azure alerts.</span></span> <span data-ttu-id="323ad-233">Bu kategorideki görür olay hello türü "myVM CPU % son 5 dakika boyunca hello 80 bırakıldı." örneğidir</span><span class="sxs-lookup"><span data-stu-id="323ad-233">An example of hello type of event you would see in this category is "CPU % on myVM has been over 80 for hello past 5 minutes."</span></span> <span data-ttu-id="323ad-234">Azure sistemleri çeşitli sahip bir uyarı verme kavramı--bir kural çeşit tanımlayabilir ve bu kural için koşullara uyan bir bildirim alıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="323ad-234">A variety of Azure systems have an alerting concept -- you can define a rule of some sort and receive a notification when conditions match that rule.</span></span> <span data-ttu-id="323ad-235">Her bir desteklenen Azure uyarı türü 'etkinleştirir,' veya hello koşullar sağlanmadığı toogenerate bir bildirim, hello etkinleştirme kaydını da hello etkinlik günlüğü toothis kategorisini gönderilir.</span><span class="sxs-lookup"><span data-stu-id="323ad-235">Each time a supported Azure alert type 'activates,' or hello conditions are met toogenerate a notification, a record of hello activation is also pushed toothis category of hello Activity Log.</span></span>

### <a name="sample-event"></a><span data-ttu-id="323ad-236">Örnek olayı</span><span class="sxs-lookup"><span data-stu-id="323ad-236">Sample event</span></span>

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in hello last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
  "eventDataId": "149d4baf-53dc-4cf4-9e29-17de37405cd9",
  "eventName": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "category": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle/events/149d4baf-53dc-4cf4-9e29-17de37405cd9/ticks/636362258535221920",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "Microsoft.ClassicCompute",
    "localizedValue": "Microsoft.ClassicCompute"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle",
  "resourceType": {
    "value": "Microsoft.ClassicCompute/domainNames/slots/roles",
    "localizedValue": "Microsoft.ClassicCompute/domainNames/slots/roles"
  },
  "operationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "operationName": {
    "value": "Microsoft.Insights/AlertRules/Resolved/Action",
    "localizedValue": "Microsoft.Insights/AlertRules/Resolved/Action"
  },
  "properties": {
    "RuleUri": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert",
    "RuleName": "myalert",
    "RuleDescription": "",
    "Threshold": "100000",
    "WindowSizeInMinutes": "5",
    "Aggregation": "Average",
    "Operator": "LessThan",
    "MetricName": "Disk read",
    "MetricUnit": "Count"
  },
  "status": {
    "value": "Resolved",
    "localizedValue": "Resolved"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T09:24:13.522192Z",
  "submissionTimestamp": "2017-07-21T09:24:15.6578651Z",
  "subscriptionId": "mySubscriptionID"
}
```

### <a name="property-descriptions"></a><span data-ttu-id="323ad-237">Özellik açıklamaları</span><span class="sxs-lookup"><span data-stu-id="323ad-237">Property descriptions</span></span>
| <span data-ttu-id="323ad-238">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="323ad-238">Element Name</span></span> | <span data-ttu-id="323ad-239">Açıklama</span><span class="sxs-lookup"><span data-stu-id="323ad-239">Description</span></span> |
| --- | --- |
| <span data-ttu-id="323ad-240">Arayan</span><span class="sxs-lookup"><span data-stu-id="323ad-240">caller</span></span> | <span data-ttu-id="323ad-241">Her zaman Microsoft.Insights/alertRules</span><span class="sxs-lookup"><span data-stu-id="323ad-241">Always Microsoft.Insights/alertRules</span></span> |
| <span data-ttu-id="323ad-242">Kanalları</span><span class="sxs-lookup"><span data-stu-id="323ad-242">channels</span></span> | <span data-ttu-id="323ad-243">Her zaman "Yönetici, işlemi"</span><span class="sxs-lookup"><span data-stu-id="323ad-243">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="323ad-244">Talepleri</span><span class="sxs-lookup"><span data-stu-id="323ad-244">claims</span></span> | <span data-ttu-id="323ad-245">JSON blob hello uyarı altyapısı hello SPN (hizmet asıl adı) ya da kaynak türüne sahip.</span><span class="sxs-lookup"><span data-stu-id="323ad-245">JSON blob with hello SPN (service principal name), or resource type, of hello alert engine.</span></span> |
| <span data-ttu-id="323ad-246">correlationId</span><span class="sxs-lookup"><span data-stu-id="323ad-246">correlationId</span></span> | <span data-ttu-id="323ad-247">Merhaba dize biçiminde bir GUID.</span><span class="sxs-lookup"><span data-stu-id="323ad-247">A GUID in hello string format.</span></span> |
| <span data-ttu-id="323ad-248">Açıklama</span><span class="sxs-lookup"><span data-stu-id="323ad-248">description</span></span> |<span data-ttu-id="323ad-249">Merhaba uyarı Olay açıklaması statik metin.</span><span class="sxs-lookup"><span data-stu-id="323ad-249">Static text description of hello alert event.</span></span> |
| <span data-ttu-id="323ad-250">eventDataId</span><span class="sxs-lookup"><span data-stu-id="323ad-250">eventDataId</span></span> |<span data-ttu-id="323ad-251">Merhaba uyarı olay benzersiz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="323ad-251">Unique identifier of hello alert event.</span></span> |
| <span data-ttu-id="323ad-252">düzeyi</span><span class="sxs-lookup"><span data-stu-id="323ad-252">level</span></span> |<span data-ttu-id="323ad-253">Merhaba olay düzeyi.</span><span class="sxs-lookup"><span data-stu-id="323ad-253">Level of hello event.</span></span> <span data-ttu-id="323ad-254">Değerleri aşağıdaki hello birini: "Kritik", "Error"Uyarı",", "Bilgi" ve "Ayrıntılı"</span><span class="sxs-lookup"><span data-stu-id="323ad-254">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="323ad-255">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="323ad-255">resourceGroupName</span></span> |<span data-ttu-id="323ad-256">Ölçüm uyarı ise hello hello kaynak grubunun adı kaynak etkilenmiş.</span><span class="sxs-lookup"><span data-stu-id="323ad-256">Name of hello resource group for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="323ad-257">Diğer uyarı türleri için bu hello hello uyarı kendisini içeren hello kaynak grubunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="323ad-257">For other alert types, this is hello name of hello resource group that contains hello alert itself.</span></span> |
| <span data-ttu-id="323ad-258">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="323ad-258">resourceProviderName</span></span> |<span data-ttu-id="323ad-259">Ölçüm uyarı ise hello kaynak sağlayıcısının adını hello için kaynak etkilenmiş.</span><span class="sxs-lookup"><span data-stu-id="323ad-259">Name of hello resource provider for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="323ad-260">Diğer uyarı türleri için bu hello hello kaynak sağlayıcısı hello uyarı kendisi için adıdır.</span><span class="sxs-lookup"><span data-stu-id="323ad-260">For other alert types, this is hello name of hello resource provider for hello alert itself.</span></span> |
| <span data-ttu-id="323ad-261">resourceId</span><span class="sxs-lookup"><span data-stu-id="323ad-261">resourceId</span></span> | <span data-ttu-id="323ad-262">Ölçüm uyarı ise hello hello kaynak kimliği adını kaynak etkilenmiş.</span><span class="sxs-lookup"><span data-stu-id="323ad-262">Name of hello resource ID for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="323ad-263">Diğer uyarı türleri için uyarı kaynağın hello kendisini hello kaynak kimliği budur.</span><span class="sxs-lookup"><span data-stu-id="323ad-263">For other alert types, this is hello resource ID of hello alert resource itself.</span></span> |
| <span data-ttu-id="323ad-264">Operationıd</span><span class="sxs-lookup"><span data-stu-id="323ad-264">operationId</span></span> |<span data-ttu-id="323ad-265">Tooa tek bir işlem karşılık gelen hello olayları arasında paylaşılan bir GUID.</span><span class="sxs-lookup"><span data-stu-id="323ad-265">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="323ad-266">operationName</span><span class="sxs-lookup"><span data-stu-id="323ad-266">operationName</span></span> |<span data-ttu-id="323ad-267">Merhaba işlemin adı.</span><span class="sxs-lookup"><span data-stu-id="323ad-267">Name of hello operation.</span></span> |
| <span data-ttu-id="323ad-268">properties</span><span class="sxs-lookup"><span data-stu-id="323ad-268">properties</span></span> |<span data-ttu-id="323ad-269">Kümesi `<Key, Value>` hello hello olay ayrıntılarını açıklayan çiftleri (diğer bir deyişle, bir sözlük).</span><span class="sxs-lookup"><span data-stu-id="323ad-269">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="323ad-270">durum</span><span class="sxs-lookup"><span data-stu-id="323ad-270">status</span></span> |<span data-ttu-id="323ad-271">Merhaba hello işlemi durumunu açıklayan dize.</span><span class="sxs-lookup"><span data-stu-id="323ad-271">String describing hello status of hello operation.</span></span> <span data-ttu-id="323ad-272">Bazı genel değerler şunlardır:, ilerleme, başarılı, başarısız, etkin, çözümlenmiş başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="323ad-272">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="323ad-273">alt durum</span><span class="sxs-lookup"><span data-stu-id="323ad-273">subStatus</span></span> | <span data-ttu-id="323ad-274">Genellikle uyarılar için null.</span><span class="sxs-lookup"><span data-stu-id="323ad-274">Usually null for alerts.</span></span> |
| <span data-ttu-id="323ad-275">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="323ad-275">eventTimestamp</span></span> |<span data-ttu-id="323ad-276">Merhaba olay hello Azure hizmetini işleme hello tarafından oluşturulan zaman damgası karşılık gelen hello olay isteği.</span><span class="sxs-lookup"><span data-stu-id="323ad-276">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="323ad-277">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="323ad-277">submissionTimestamp</span></span> |<span data-ttu-id="323ad-278">Merhaba olay sorgulama için kullanılabilir duruma zaman damgası.</span><span class="sxs-lookup"><span data-stu-id="323ad-278">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="323ad-279">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="323ad-279">subscriptionId</span></span> |<span data-ttu-id="323ad-280">Azure abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="323ad-280">Azure Subscription Id.</span></span> |

### <a name="properties-field-per-alert-type"></a><span data-ttu-id="323ad-281">Uyarı türü başına özellikleri alanı</span><span class="sxs-lookup"><span data-stu-id="323ad-281">Properties field per alert type</span></span>
<span data-ttu-id="323ad-282">Merhaba özellikleri alanı hello uyarı olayının hello kaynağı bağlı olarak farklı değerler içerir.</span><span class="sxs-lookup"><span data-stu-id="323ad-282">hello properties field will contain different values depending on hello source of hello alert event.</span></span> <span data-ttu-id="323ad-283">İki ortak uyarı Olay Etkinlik günlüğü uyarıları ve ölçüm uyarıları sağlayıcılarıdır.</span><span class="sxs-lookup"><span data-stu-id="323ad-283">Two common alert event providers are Activity Log alerts and metric alerts.</span></span>

#### <a name="properties-for-activity-log-alerts"></a><span data-ttu-id="323ad-284">Etkinlik günlüğü uyarıların özellikleri</span><span class="sxs-lookup"><span data-stu-id="323ad-284">Properties for Activity Log alerts</span></span>
| <span data-ttu-id="323ad-285">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="323ad-285">Element Name</span></span> | <span data-ttu-id="323ad-286">Açıklama</span><span class="sxs-lookup"><span data-stu-id="323ad-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="323ad-287">properties.subscriptionId</span><span class="sxs-lookup"><span data-stu-id="323ad-287">properties.subscriptionId</span></span> | <span data-ttu-id="323ad-288">etkinleştirilen bu etkinlik günlüğü uyarı kuralı toobe neden hello etkinlik günlüğü olayı Hello abonelik kimliği.</span><span class="sxs-lookup"><span data-stu-id="323ad-288">hello subscription ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="323ad-289">properties.eventDataId</span><span class="sxs-lookup"><span data-stu-id="323ad-289">properties.eventDataId</span></span> | <span data-ttu-id="323ad-290">Merhaba olay verileri Kimliğinden etkinleştirilen bu etkinlik günlüğü uyarı kuralı toobe neden hello etkinlik günlüğü olayı.</span><span class="sxs-lookup"><span data-stu-id="323ad-290">hello event data ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="323ad-291">properties.resourceGroup</span><span class="sxs-lookup"><span data-stu-id="323ad-291">properties.resourceGroup</span></span> | <span data-ttu-id="323ad-292">Kaynak grubundan etkinleştirilen bu etkinlik günlüğü uyarı kuralı toobe neden hello etkinlik günlüğü olayı Hello.</span><span class="sxs-lookup"><span data-stu-id="323ad-292">hello resource group from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="323ad-293">properties.resourceId</span><span class="sxs-lookup"><span data-stu-id="323ad-293">properties.resourceId</span></span> | <span data-ttu-id="323ad-294">etkinleştirilen bu etkinlik günlüğü uyarı kuralı toobe neden hello etkinlik günlüğü olayı Hello kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="323ad-294">hello resource ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="323ad-295">properties.eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="323ad-295">properties.eventTimestamp</span></span> | <span data-ttu-id="323ad-296">etkinleştirilen bu etkinlik günlüğü uyarı kuralı toobe neden hello etkinlik günlüğü olay Hello olay zaman damgası.</span><span class="sxs-lookup"><span data-stu-id="323ad-296">hello event timestamp of hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="323ad-297">properties.operationName</span><span class="sxs-lookup"><span data-stu-id="323ad-297">properties.operationName</span></span> | <span data-ttu-id="323ad-298">etkinleştirilen bu etkinlik günlüğü uyarı kuralı toobe neden hello etkinlik günlüğü olayı Hello işlemi adı.</span><span class="sxs-lookup"><span data-stu-id="323ad-298">hello operation name from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="323ad-299">Properties.Status</span><span class="sxs-lookup"><span data-stu-id="323ad-299">properties.status</span></span> | <span data-ttu-id="323ad-300">etkinleştirilen bu etkinlik günlüğü uyarı kuralı toobe neden hello etkinlik günlüğü olayı durumundan Hello.</span><span class="sxs-lookup"><span data-stu-id="323ad-300">hello status from hello activity log event which caused this activity log alert rule toobe activated.</span></span>|

#### <a name="properties-for-metric-alerts"></a><span data-ttu-id="323ad-301">Ölçüm uyarıların özellikleri</span><span class="sxs-lookup"><span data-stu-id="323ad-301">Properties for metric alerts</span></span>
| <span data-ttu-id="323ad-302">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="323ad-302">Element Name</span></span> | <span data-ttu-id="323ad-303">Açıklama</span><span class="sxs-lookup"><span data-stu-id="323ad-303">Description</span></span> |
| --- | --- |
| <span data-ttu-id="323ad-304">Özellikler. RuleUri</span><span class="sxs-lookup"><span data-stu-id="323ad-304">properties.RuleUri</span></span> | <span data-ttu-id="323ad-305">Merhaba ölçüm uyarı kuralı kendisini kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="323ad-305">Resource ID of hello metric alert rule itself.</span></span> |
| <span data-ttu-id="323ad-306">Özellikler. RuleName</span><span class="sxs-lookup"><span data-stu-id="323ad-306">properties.RuleName</span></span> | <span data-ttu-id="323ad-307">Merhaba ölçüm uyarı kuralı Hello adı.</span><span class="sxs-lookup"><span data-stu-id="323ad-307">hello name of hello metric alert rule.</span></span> |
| <span data-ttu-id="323ad-308">Özellikler. RuleDescription</span><span class="sxs-lookup"><span data-stu-id="323ad-308">properties.RuleDescription</span></span> | <span data-ttu-id="323ad-309">Merhaba ölçüm uyarı kuralı (Merhaba uyarı kuralı tanımlanan) Hello açıklaması.</span><span class="sxs-lookup"><span data-stu-id="323ad-309">hello description of hello metric alert rule (as defined in hello alert rule).</span></span> |
| <span data-ttu-id="323ad-310">Özellikler. Eşik</span><span class="sxs-lookup"><span data-stu-id="323ad-310">properties.Threshold</span></span> | <span data-ttu-id="323ad-311">Merhaba ölçüm uyarı kuralı Hello hesaplanmasında kullanılan hello eşik değeri.</span><span class="sxs-lookup"><span data-stu-id="323ad-311">hello threshold value used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="323ad-312">Özellikler. WindowSizeInMinutes</span><span class="sxs-lookup"><span data-stu-id="323ad-312">properties.WindowSizeInMinutes</span></span> | <span data-ttu-id="323ad-313">Merhaba ölçüm uyarı kuralı Hello hesaplanmasında kullanılan hello pencere boyutu.</span><span class="sxs-lookup"><span data-stu-id="323ad-313">hello window size used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="323ad-314">Özellikler. Toplama</span><span class="sxs-lookup"><span data-stu-id="323ad-314">properties.Aggregation</span></span> | <span data-ttu-id="323ad-315">Merhaba ölçüm uyarı kuralda tanımlanan hello toplama türü.</span><span class="sxs-lookup"><span data-stu-id="323ad-315">hello aggregation type defined in hello metric alert rule.</span></span> |
| <span data-ttu-id="323ad-316">Özellikler. İşleci</span><span class="sxs-lookup"><span data-stu-id="323ad-316">properties.Operator</span></span> | <span data-ttu-id="323ad-317">Merhaba ölçüm uyarı kuralı Hello hesaplanmasında kullanılan hello koşullu işleç.</span><span class="sxs-lookup"><span data-stu-id="323ad-317">hello conditional operator used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="323ad-318">Özellikler. MetricName</span><span class="sxs-lookup"><span data-stu-id="323ad-318">properties.MetricName</span></span> | <span data-ttu-id="323ad-319">Merhaba hello ölçüm uyarı kuralı hello hesaplanmasında kullanılan hello ölçüsünün ölçüm adı.</span><span class="sxs-lookup"><span data-stu-id="323ad-319">hello metric name of hello metric used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="323ad-320">Özellikler. MetricUnit</span><span class="sxs-lookup"><span data-stu-id="323ad-320">properties.MetricUnit</span></span> | <span data-ttu-id="323ad-321">ölçü birimi hello ölçüm uyarı kuralı hello hesaplanmasında kullanılan hello ölçümünü Hello.</span><span class="sxs-lookup"><span data-stu-id="323ad-321">hello metric unit for hello metric used in hello evaluation of hello metric alert rule.</span></span> |

## <a name="autoscale"></a><span data-ttu-id="323ad-322">Otomatik Ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="323ad-322">Autoscale</span></span>
<span data-ttu-id="323ad-323">Bu kategori, aboneliğinizde tanımladığınız herhangi bir otomatik ölçeklendirme ayarı göre hello otomatik ölçeklendirme altyapısının herhangi bir olayları ilgili toohello işlem hello kaydını içerir.</span><span class="sxs-lookup"><span data-stu-id="323ad-323">This category contains hello record of any events related toohello operation of hello autoscale engine based on any autoscale settings you have defined in your subscription.</span></span> <span data-ttu-id="323ad-324">Bu kategorideki görür olay hello türü "Otomatik ölçeklendirme ölçek büyütme eylemi başarısız oldu." örneğidir</span><span class="sxs-lookup"><span data-stu-id="323ad-324">An example of hello type of event you would see in this category is "Autoscale scale up action failed."</span></span> <span data-ttu-id="323ad-325">Otomatik ölçeklendirme'ni kullanarak, otomatik olarak ölçeğini veya ölçeklendirmek hello desteklenen kaynak türü örneği sayısı dayalı bir otomatik ölçeklendirme ayarı kullanarak gün ve/veya yük (ölçüm) verileri zamanında.</span><span class="sxs-lookup"><span data-stu-id="323ad-325">Using autoscale, you can automatically scale out or scale in hello number of instances in a supported resource type based on time of day and/or load (metric) data using an autoscale setting.</span></span> <span data-ttu-id="323ad-326">Hello koşullar karşılandığında tooscale yukarı veya aşağı başlangıç hello ve başarılı veya başarısız olayları bu kategorideki kaydedilmez.</span><span class="sxs-lookup"><span data-stu-id="323ad-326">When hello conditions are met tooscale up or down, hello start and succeeded or failed events will be recorded in this category.</span></span>

### <a name="sample-event"></a><span data-ttu-id="323ad-327">Örnek olayı</span><span class="sxs-lookup"><span data-stu-id="323ad-327">Sample event</span></span>
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
  "eventDataId": "a5b92075-1de9-42f1-b52e-6f3e4945a7c7",
  "eventName": {
    "value": "AutoscaleAction",
    "localizedValue": "AutoscaleAction"
  },
  "category": {
    "value": "Autoscale",
    "localizedValue": "Autoscale"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup/events/a5b92075-1de9-42f1-b52e-6f3e4945a7c7/ticks/636361956518681572",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "microsoft.insights",
    "localizedValue": "microsoft.insights"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup",
  "resourceType": {
    "value": "microsoft.insights/autoscalesettings",
    "localizedValue": "microsoft.insights/autoscalesettings"
  },
  "operationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "operationName": {
    "value": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action",
    "localizedValue": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action"
  },
  "properties": {
    "Description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
    "ResourceName": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource",
    "OldInstancesCount": "3",
    "NewInstancesCount": "2",
    "LastScaleActionTime": "Fri, 21 Jul 2017 01:00:51 GMT"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T01:00:51.8681572Z",
  "submissionTimestamp": "2017-07-21T01:00:52.3008754Z",
  "subscriptionId": "mySubscriptionID"
}

```

### <a name="property-descriptions"></a><span data-ttu-id="323ad-328">Özellik açıklamaları</span><span class="sxs-lookup"><span data-stu-id="323ad-328">Property descriptions</span></span>
| <span data-ttu-id="323ad-329">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="323ad-329">Element Name</span></span> | <span data-ttu-id="323ad-330">Açıklama</span><span class="sxs-lookup"><span data-stu-id="323ad-330">Description</span></span> |
| --- | --- |
| <span data-ttu-id="323ad-331">Arayan</span><span class="sxs-lookup"><span data-stu-id="323ad-331">caller</span></span> | <span data-ttu-id="323ad-332">Her zaman Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="323ad-332">Always Microsoft.Insights/autoscaleSettings</span></span> |
| <span data-ttu-id="323ad-333">Kanalları</span><span class="sxs-lookup"><span data-stu-id="323ad-333">channels</span></span> | <span data-ttu-id="323ad-334">Her zaman "Yönetici, işlemi"</span><span class="sxs-lookup"><span data-stu-id="323ad-334">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="323ad-335">Talepleri</span><span class="sxs-lookup"><span data-stu-id="323ad-335">claims</span></span> | <span data-ttu-id="323ad-336">JSON blob hello hello otomatik ölçeklendirme altyapısı SPN (hizmet asıl adı) ya da kaynak türüne sahip.</span><span class="sxs-lookup"><span data-stu-id="323ad-336">JSON blob with hello SPN (service principal name), or resource type, of hello autoscale engine.</span></span> |
| <span data-ttu-id="323ad-337">correlationId</span><span class="sxs-lookup"><span data-stu-id="323ad-337">correlationId</span></span> | <span data-ttu-id="323ad-338">Merhaba dize biçiminde bir GUID.</span><span class="sxs-lookup"><span data-stu-id="323ad-338">A GUID in hello string format.</span></span> |
| <span data-ttu-id="323ad-339">Açıklama</span><span class="sxs-lookup"><span data-stu-id="323ad-339">description</span></span> |<span data-ttu-id="323ad-340">Merhaba otomatik ölçeklendirme Olay açıklaması statik metin.</span><span class="sxs-lookup"><span data-stu-id="323ad-340">Static text description of hello autoscale event.</span></span> |
| <span data-ttu-id="323ad-341">eventDataId</span><span class="sxs-lookup"><span data-stu-id="323ad-341">eventDataId</span></span> |<span data-ttu-id="323ad-342">Merhaba otomatik ölçeklendirme olay benzersiz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="323ad-342">Unique identifier of hello autoscale event.</span></span> |
| <span data-ttu-id="323ad-343">düzeyi</span><span class="sxs-lookup"><span data-stu-id="323ad-343">level</span></span> |<span data-ttu-id="323ad-344">Merhaba olay düzeyi.</span><span class="sxs-lookup"><span data-stu-id="323ad-344">Level of hello event.</span></span> <span data-ttu-id="323ad-345">Değerleri aşağıdaki hello birini: "Kritik", "Error"Uyarı",", "Bilgi" ve "Ayrıntılı"</span><span class="sxs-lookup"><span data-stu-id="323ad-345">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="323ad-346">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="323ad-346">resourceGroupName</span></span> |<span data-ttu-id="323ad-347">Merhaba otomatik ölçeklendirme ayarı hello kaynak grubunun adı.</span><span class="sxs-lookup"><span data-stu-id="323ad-347">Name of hello resource group for hello autoscale setting.</span></span> |
| <span data-ttu-id="323ad-348">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="323ad-348">resourceProviderName</span></span> |<span data-ttu-id="323ad-349">Merhaba otomatik ölçeklendirme ayarı hello kaynak sağlayıcısı adı.</span><span class="sxs-lookup"><span data-stu-id="323ad-349">Name of hello resource provider for hello autoscale setting.</span></span> |
| <span data-ttu-id="323ad-350">resourceId</span><span class="sxs-lookup"><span data-stu-id="323ad-350">resourceId</span></span> |<span data-ttu-id="323ad-351">Merhaba otomatik ölçeklendirme ayarı kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="323ad-351">Resource id of hello autoscale setting.</span></span> |
| <span data-ttu-id="323ad-352">Operationıd</span><span class="sxs-lookup"><span data-stu-id="323ad-352">operationId</span></span> |<span data-ttu-id="323ad-353">Tooa tek bir işlem karşılık gelen hello olayları arasında paylaşılan bir GUID.</span><span class="sxs-lookup"><span data-stu-id="323ad-353">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="323ad-354">operationName</span><span class="sxs-lookup"><span data-stu-id="323ad-354">operationName</span></span> |<span data-ttu-id="323ad-355">Merhaba işlemin adı.</span><span class="sxs-lookup"><span data-stu-id="323ad-355">Name of hello operation.</span></span> |
| <span data-ttu-id="323ad-356">properties</span><span class="sxs-lookup"><span data-stu-id="323ad-356">properties</span></span> |<span data-ttu-id="323ad-357">Kümesi `<Key, Value>` hello hello olay ayrıntılarını açıklayan çiftleri (diğer bir deyişle, bir sözlük).</span><span class="sxs-lookup"><span data-stu-id="323ad-357">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="323ad-358">Özellikler. Açıklama</span><span class="sxs-lookup"><span data-stu-id="323ad-358">properties.Description</span></span> | <span data-ttu-id="323ad-359">Hangi hello otomatik ölçeklendirme altyapısı yapmakta olduğu ayrıntılı açıklaması.</span><span class="sxs-lookup"><span data-stu-id="323ad-359">Detailed description of what hello autoscale engine was doing.</span></span> |
| <span data-ttu-id="323ad-360">Özellikler. ResourceName</span><span class="sxs-lookup"><span data-stu-id="323ad-360">properties.ResourceName</span></span> | <span data-ttu-id="323ad-361">Kaynak Kimliğini hello etkilenen kaynak (üzerinde hangi hello ölçek eylemi gerçekleştirilir kaynak hello)</span><span class="sxs-lookup"><span data-stu-id="323ad-361">Resource ID of hello impacted resource (hello resource on which hello scale action was being performed)</span></span> |
| <span data-ttu-id="323ad-362">Özellikler. OldInstancesCount</span><span class="sxs-lookup"><span data-stu-id="323ad-362">properties.OldInstancesCount</span></span> | <span data-ttu-id="323ad-363">Merhaba hello otomatik ölçeklendirme eylemi önce örneklerinin sayısını etkisi sürdü.</span><span class="sxs-lookup"><span data-stu-id="323ad-363">hello number of instances before hello autoscale action took effect.</span></span> |
| <span data-ttu-id="323ad-364">Özellikler. NewInstancesCount</span><span class="sxs-lookup"><span data-stu-id="323ad-364">properties.NewInstancesCount</span></span> | <span data-ttu-id="323ad-365">Merhaba hello otomatik ölçeklendirme eylemin etkisi sonra örneği sayısı.</span><span class="sxs-lookup"><span data-stu-id="323ad-365">hello number of instances after hello autoscale action took effect.</span></span> |
| <span data-ttu-id="323ad-366">Özellikler. LastScaleActionTime</span><span class="sxs-lookup"><span data-stu-id="323ad-366">properties.LastScaleActionTime</span></span> | <span data-ttu-id="323ad-367">Merhaba otomatik ölçeklendirme eylemi gerçekleştiği, hello zaman damgası.</span><span class="sxs-lookup"><span data-stu-id="323ad-367">hello timestamp of when hello autoscale action occurred.</span></span> |
| <span data-ttu-id="323ad-368">durum</span><span class="sxs-lookup"><span data-stu-id="323ad-368">status</span></span> |<span data-ttu-id="323ad-369">Merhaba hello işlemi durumunu açıklayan dize.</span><span class="sxs-lookup"><span data-stu-id="323ad-369">String describing hello status of hello operation.</span></span> <span data-ttu-id="323ad-370">Bazı genel değerler şunlardır:, ilerleme, başarılı, başarısız, etkin, çözümlenmiş başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="323ad-370">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="323ad-371">alt durum</span><span class="sxs-lookup"><span data-stu-id="323ad-371">subStatus</span></span> | <span data-ttu-id="323ad-372">Genellikle otomatik ölçeklendirme için null.</span><span class="sxs-lookup"><span data-stu-id="323ad-372">Usually null for autoscale.</span></span> |
| <span data-ttu-id="323ad-373">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="323ad-373">eventTimestamp</span></span> |<span data-ttu-id="323ad-374">Merhaba olay hello Azure hizmetini işleme hello tarafından oluşturulan zaman damgası karşılık gelen hello olay isteği.</span><span class="sxs-lookup"><span data-stu-id="323ad-374">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="323ad-375">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="323ad-375">submissionTimestamp</span></span> |<span data-ttu-id="323ad-376">Merhaba olay sorgulama için kullanılabilir duruma zaman damgası.</span><span class="sxs-lookup"><span data-stu-id="323ad-376">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="323ad-377">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="323ad-377">subscriptionId</span></span> |<span data-ttu-id="323ad-378">Azure abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="323ad-378">Azure Subscription Id.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="323ad-379">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="323ad-379">Next steps</span></span>
* [<span data-ttu-id="323ad-380">Merhaba etkinlik günlüğü (önceki adıyla denetim günlüklerini) hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="323ad-380">Learn more about hello Activity Log (formerly Audit Logs)</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="323ad-381">Hello Azure etkinlik günlüğü tooEvent hub akışı</span><span class="sxs-lookup"><span data-stu-id="323ad-381">Stream hello Azure Activity Log tooEvent Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
