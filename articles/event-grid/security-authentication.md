---
title: "aaaAzure olay kılavuz güvenlik ve kimlik doğrulama"
description: "Azure olay kılavuz ve onun kavramlarını açıklar."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/14/2017
ms.author: babanisa
ms.openlocfilehash: 74f692c7e3a30856c3a80cbbfe82a26bf4c1c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-security-and-authentication"></a><span data-ttu-id="b2523-103">Olay kılavuz güvenlik ve kimlik doğrulama</span><span class="sxs-lookup"><span data-stu-id="b2523-103">Event Grid security and authentication</span></span> 

<span data-ttu-id="b2523-104">Azure olay kılavuz üç tür kimlik doğrulama vardır:</span><span class="sxs-lookup"><span data-stu-id="b2523-104">Azure Event Grid has three types of authentication:</span></span>

* <span data-ttu-id="b2523-105">Olay abonelikleri</span><span class="sxs-lookup"><span data-stu-id="b2523-105">Event subscriptions</span></span>
* <span data-ttu-id="b2523-106">Olay yayımlama</span><span class="sxs-lookup"><span data-stu-id="b2523-106">Event publishing</span></span>
* <span data-ttu-id="b2523-107">Web kancası olay teslimi</span><span class="sxs-lookup"><span data-stu-id="b2523-107">WebHook event delivery</span></span>

## <a name="webhook-event-delivery"></a><span data-ttu-id="b2523-108">Web kancası olay teslimi</span><span class="sxs-lookup"><span data-stu-id="b2523-108">WebHook Event delivery</span></span>

<span data-ttu-id="b2523-109">Web kancası Azure olay kılavuz gelen gerçek zamanlı birçok yolu tooreceive olayları biridir.</span><span class="sxs-lookup"><span data-stu-id="b2523-109">Webhooks are one of many ways tooreceive events in real time from Azure Event Grid.</span></span>

<span data-ttu-id="b2523-110">Olduğundan her zaman teslim yeni bir olay hazır toobe, olay kılavuz hello gövdesinde tooyour Web kancası hello olay ile birlikte bir HTTP isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="b2523-110">Every time there is a new event ready toobe delivered, Event Grid sends an HTTP request with tooyour WebHook with hello event in hello body.</span></span>

<span data-ttu-id="b2523-111">Olay kılavuzla kendi Web kancası uç noktasını kaydetme zaman, basit bir doğrulama kodu içeren bir POST isteği sipariş tooprove uç nokta sahipliği gönderir.</span><span class="sxs-lookup"><span data-stu-id="b2523-111">When you register your own WebHook endpoint with Event Grid, it sends you a POST request with a simple validation code in order tooprove endpoint ownership.</span></span> <span data-ttu-id="b2523-112">Uygulamanızın arka hello doğrulama kodu Yankı tarafından toorespond gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2523-112">Your app needs toorespond by echoing back hello validation code.</span></span> <span data-ttu-id="b2523-113">Olay kılavuz olayları hello doğrulama geçmedi tooWebHook uç noktaları teslim değil.</span><span class="sxs-lookup"><span data-stu-id="b2523-113">Event Grid will not deliver events tooWebHook endpoints that have not passed hello validation.</span></span>
 
### <a name="validation-details"></a><span data-ttu-id="b2523-114">Doğrulama ayrıntıları:</span><span class="sxs-lookup"><span data-stu-id="b2523-114">Validation details:</span></span>

* <span data-ttu-id="b2523-115">Olay aboneliği oluşturma/güncelleştirme Hello sırasında bir "SubscriptionValidationEvent" olay toohello hedef uç noktası olay kılavuz gönderir.</span><span class="sxs-lookup"><span data-stu-id="b2523-115">At hello time of event subscription creation/update, Event Grid posts a “SubscriptionValidationEvent” event toohello target endpoint.</span></span>
* <span data-ttu-id="b2523-116">bir üstbilgi değeri "Olay türü: doğrulama" Merhaba olayı içerir.</span><span class="sxs-lookup"><span data-stu-id="b2523-116">hello event contains a header value “Event-Type: Validation”.</span></span>
* <span data-ttu-id="b2523-117">Merhaba olay gövdesi olan hello diğer olay kılavuz olaylarla aynı şema.</span><span class="sxs-lookup"><span data-stu-id="b2523-117">hello event body has hello same schema as other Event Grid events.</span></span>
* <span data-ttu-id="b2523-118">Merhaba olay verilerini bir "ValidationCode" özelliği rastgele oluşturulmuş bir dizeyle örneğin içerir "ValidationCode: acb13...".</span><span class="sxs-lookup"><span data-stu-id="b2523-118">hello event data includes a “ValidationCode” property with a randomly generated string e.g. “ValidationCode: acb13…”.</span></span>

<span data-ttu-id="b2523-119">Sipariş tooprove uç nokta sahipliği geri hello doğrulama kodu örneğin echo "ValidationResponse: acb13...".</span><span class="sxs-lookup"><span data-stu-id="b2523-119">In order tooprove endpoint ownership, echo back hello validation code e.g “ValidationResponse: acb13…”.</span></span>

<span data-ttu-id="b2523-120">Son olarak, Azure olay kılavuz yalnızca HTTPS Web kancası uç noktaları desteklediğini önemli toonote olur.</span><span class="sxs-lookup"><span data-stu-id="b2523-120">Finally, it is important toonote that Azure Event Grid only supports HTTPS webhook endpoints.</span></span>
## <a name="event-subscription"></a><span data-ttu-id="b2523-121">Olay aboneliği</span><span class="sxs-lookup"><span data-stu-id="b2523-121">Event subscription</span></span>

<span data-ttu-id="b2523-122">toosubscribe tooan olay hello olmalıdır **Microsoft.EventGrid/EventSubscriptions/Write** hello izni gerekli kaynak.</span><span class="sxs-lookup"><span data-stu-id="b2523-122">toosubscribe tooan event, you must have hello **Microsoft.EventGrid/EventSubscriptions/Write** permission on hello required resource.</span></span> <span data-ttu-id="b2523-123">Merhaba kapsamda yeni bir abonelik hello kaynağının yazma için bu izni gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="b2523-123">You need this permission because you are writing a new subscription at hello scope of hello resource.</span></span> <span data-ttu-id="b2523-124">Merhaba, kaynak tooa sistem konu veya özel konuyu abone göre farklı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b2523-124">hello required resource differs based on whether you are subscribing tooa system topic or custom topic.</span></span> <span data-ttu-id="b2523-125">Her iki tür, bu bölümde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b2523-125">Both types are described in this section.</span></span>

### <a name="system-topics-azure-service-publishers"></a><span data-ttu-id="b2523-126">Sistem konuları (Azure hizmeti yayımcılar)</span><span class="sxs-lookup"><span data-stu-id="b2523-126">System topics (Azure service publishers)</span></span>

<span data-ttu-id="b2523-127">Sistem konuları için izni toowrite hello kapsam hello kaynak yayımlama hello olayının yeni bir olay abonelik gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2523-127">For system topics, you need permission toowrite a new event subscription at hello scope of hello resource publishing hello event.</span></span> <span data-ttu-id="b2523-128">Merhaba kaynağının Hello biçimdedir:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span><span class="sxs-lookup"><span data-stu-id="b2523-128">hello format of hello resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span></span>

<span data-ttu-id="b2523-129">Örneğin, toosubscribe tooan olay adlı bir depolama hesabında **myacct**, üzerinde hello Microsoft.EventGrid/EventSubscriptions/Write izniniz olmalıdır:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span><span class="sxs-lookup"><span data-stu-id="b2523-129">For example, toosubscribe tooan event on a storage account named **myacct**, you need hello Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span></span>

### <a name="custom-topics"></a><span data-ttu-id="b2523-130">Özel konular</span><span class="sxs-lookup"><span data-stu-id="b2523-130">Custom topics</span></span>

<span data-ttu-id="b2523-131">Özel konular için izni toowrite hello kapsam hello olay kılavuz konusunun yeni bir olay abonelik gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2523-131">For custom topics, you need permission toowrite a new event subscription at hello scope of hello Event Grid topic.</span></span> <span data-ttu-id="b2523-132">Merhaba kaynağının Hello biçimdedir:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span><span class="sxs-lookup"><span data-stu-id="b2523-132">hello format of hello resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span></span>

<span data-ttu-id="b2523-133">Adlı Örneğin, toosubscribe tooa özel konu **mytopic**, üzerinde hello Microsoft.EventGrid/EventSubscriptions/Write izniniz olmalıdır:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span><span class="sxs-lookup"><span data-stu-id="b2523-133">For example, toosubscribe tooa custom topic named **mytopic**, you need hello Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span></span>

## <a name="topic-publishing"></a><span data-ttu-id="b2523-134">Konu yayımlama</span><span class="sxs-lookup"><span data-stu-id="b2523-134">Topic publishing</span></span>

<span data-ttu-id="b2523-135">Konular, paylaşılan erişim imzası (SAS) veya anahtar kimlik doğrulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="b2523-135">Topics use either Shared Access Signature (SAS) or key authentication.</span></span> <span data-ttu-id="b2523-136">SAS öneririz, ancak anahtar kimlik doğrulaması basit programlama sağlar ve birçok varolan Web kancası yayımcıları ile uyumludur.</span><span class="sxs-lookup"><span data-stu-id="b2523-136">We recommend SAS, but key authentication provides simple programming, and is compatible with many existing webhook publishers.</span></span> 

<span data-ttu-id="b2523-137">Merhaba HTTP üstbilgisinde hello kimlik doğrulama değeri içerir.</span><span class="sxs-lookup"><span data-stu-id="b2523-137">You include hello authentication value in hello HTTP header.</span></span> <span data-ttu-id="b2523-138">SA'ları için kullanmak **aeg sas belirteci** hello üstbilgi değeri.</span><span class="sxs-lookup"><span data-stu-id="b2523-138">For SAS, use **aeg-sas-token** for hello header value.</span></span> <span data-ttu-id="b2523-139">Anahtar kimlik doğrulaması için kullanmak **aeg sas anahtarı** hello üstbilgi değeri.</span><span class="sxs-lookup"><span data-stu-id="b2523-139">For key authentication, use **aeg-sas-key** for hello header value.</span></span>

### <a name="key-authentication"></a><span data-ttu-id="b2523-140">Anahtar kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="b2523-140">Key authentication</span></span>

<span data-ttu-id="b2523-141">Anahtar kimlik doğrulaması hello Basit kimlik doğrulama biçimidir.</span><span class="sxs-lookup"><span data-stu-id="b2523-141">Key authentication is hello simplest form of authentication.</span></span> <span data-ttu-id="b2523-142">Merhaba biçimi kullanın:`aeg-sas-key: <your key>`</span><span class="sxs-lookup"><span data-stu-id="b2523-142">Use hello format: `aeg-sas-key: <your key>`</span></span>

<span data-ttu-id="b2523-143">Örneğin, bir anahtar ile geçirin:</span><span class="sxs-lookup"><span data-stu-id="b2523-143">For example, you pass a key with:</span></span> 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a><span data-ttu-id="b2523-144">SAS belirteçleri</span><span class="sxs-lookup"><span data-stu-id="b2523-144">SAS tokens</span></span>

<span data-ttu-id="b2523-145">Olay kılavuz için SAS belirteci hello kaynak, bir sona erme zamanı ve imza içerir.</span><span class="sxs-lookup"><span data-stu-id="b2523-145">SAS tokens for Event Grid include hello resource, an expiration time, and a signature.</span></span> <span data-ttu-id="b2523-146">Merhaba hello SAS belirteci biçimi şöyledir: `r={resource}&e={expiration}&s={signature}`.</span><span class="sxs-lookup"><span data-stu-id="b2523-146">hello format of hello SAS token is: `r={resource}&e={expiration}&s={signature}`.</span></span>

<span data-ttu-id="b2523-147">Merhaba kaynak hello yoludur hello konu toowhich için olayları gönderiyor.</span><span class="sxs-lookup"><span data-stu-id="b2523-147">hello resource is hello path for hello topic toowhich you are sending events.</span></span> <span data-ttu-id="b2523-148">Örneğin, geçerli bir kaynak yolu şöyledir:`https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span><span class="sxs-lookup"><span data-stu-id="b2523-148">For example, a valid resource path is: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span></span>

<span data-ttu-id="b2523-149">Merhaba imza bir anahtarı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b2523-149">You generate hello signature from a key.</span></span>

<span data-ttu-id="b2523-150">Örneğin, geçerli **aeg sas belirteci** değer:</span><span class="sxs-lookup"><span data-stu-id="b2523-150">For example, a valid **aeg-sas-token** value is:</span></span>

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

<span data-ttu-id="b2523-151">Aşağıdaki örneğine hello olay kılavuz ile kullanmak için bir SAS belirteci oluşturur:</span><span class="sxs-lookup"><span data-stu-id="b2523-151">hello following example creates a SAS token for use with Event Grid:</span></span>

```cs
static string BuildSharedAccessSignature(string resource, DateTime expirationUtc, string key)
{
    const char Resource = 'r';
    const char Expiration = 'e';
    const char Signature = 's';

    string encodedResource = HttpUtility.UrlEncode(resource);
    string encodedExpirationUtc = HttpUtility.UrlEncode(expirationUtc.ToString());

    string unsignedSas = $"{Resource}={encodedResource}&{Expiration}={encodedExpirationUtc}";
    using (var hmac = new HMACSHA256(Convert.FromBase64String(key)))
    {
        string signature = Convert.ToBase64String(hmac.ComputeHash(Encoding.UTF8.GetBytes(unsignedSas)));
        string encodedSignature = HttpUtility.UrlEncode(signature);
        string signedSas = $"{unsignedSas}&{Signature}={encodedSignature}";

        return signedSas;
    }
}
```

## <a name="management-access-control"></a><span data-ttu-id="b2523-152">Yönetim erişim denetimi</span><span class="sxs-lookup"><span data-stu-id="b2523-152">Management Access Control</span></span>

<span data-ttu-id="b2523-153">Azure olay kılavuz, toocontrol hello düzeyini verilen erişim toodifferent kullanıcılar toodo listesi olay abonelikleri gibi çeşitli yönetim işlemlerini sağlar. Yeni kampanya oluşturmak ve anahtarları oluştur.</span><span class="sxs-lookup"><span data-stu-id="b2523-153">Azure Event Grid allows you toocontrol hello level of access given toodifferent users toodo various management operations such as list event subscriptions, create new ones, and generate keys.</span></span> <span data-ttu-id="b2523-154">Bu olay kılavuz Azure'nın rol tabanlı erişim denetleyin (RBAC) kullanır.</span><span class="sxs-lookup"><span data-stu-id="b2523-154">Event Grid utilizes Azure's Role Based Access Check (RBAC) for this.</span></span>

### <a name="operation-types"></a><span data-ttu-id="b2523-155">İşlem türleri</span><span class="sxs-lookup"><span data-stu-id="b2523-155">Operation types</span></span>

<span data-ttu-id="b2523-156">Azure olay kılavuz hello aşağıdaki eylemleri destekler:</span><span class="sxs-lookup"><span data-stu-id="b2523-156">Azure event grid supports hello following actions:</span></span>

* <span data-ttu-id="b2523-157">Microsoft.EventGrid/*/read</span><span class="sxs-lookup"><span data-stu-id="b2523-157">Microsoft.EventGrid/*/read</span></span> 
* <span data-ttu-id="b2523-158">Microsoft.EventGrid/*/write</span><span class="sxs-lookup"><span data-stu-id="b2523-158">Microsoft.EventGrid/*/write</span></span> 
* <span data-ttu-id="b2523-159">Microsoft.EventGrid/*/delete</span><span class="sxs-lookup"><span data-stu-id="b2523-159">Microsoft.EventGrid/*/delete</span></span> 
* <span data-ttu-id="b2523-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span><span class="sxs-lookup"><span data-stu-id="b2523-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span></span> 
* <span data-ttu-id="b2523-161">Microsoft.EventGrid/topics/listKeys/action</span><span class="sxs-lookup"><span data-stu-id="b2523-161">Microsoft.EventGrid/topics/listKeys/action</span></span> 
* <span data-ttu-id="b2523-162">Microsoft.EventGrid/topics/regenerateKey/action</span><span class="sxs-lookup"><span data-stu-id="b2523-162">Microsoft.EventGrid/topics/regenerateKey/action</span></span>

<span data-ttu-id="b2523-163">normal okuma işlemleri dışında filtrelenmiş son üç işlemleri dönüş olası gizli bilgi hello.</span><span class="sxs-lookup"><span data-stu-id="b2523-163">hello last three operations return potentially secret information which gets filtered out of normal read operations.</span></span> <span data-ttu-id="b2523-164">Bu, toorestrict erişim toothese işlemleri için en iyi uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="b2523-164">It is best practice for you toorestrict access toothese operations.</span></span> <span data-ttu-id="b2523-165">Özel roller kullanılarak oluşturulabilir [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure komut satırı arabirimi (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md)ve hello [REST API](../active-directory/role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="b2523-165">Custom roles can be created using [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md), and hello [REST API](../active-directory/role-based-access-control-manage-access-rest.md).</span></span>

### <a name="enforcing-role-based-access-check-rbac"></a><span data-ttu-id="b2523-166">Rol uygulamaya dayalı erişim denetimi (RBAC)</span><span class="sxs-lookup"><span data-stu-id="b2523-166">Enforcing Role Based Access Check (RBAC)</span></span>

<span data-ttu-id="b2523-167">Farklı kullanıcılar için adımları tooenforce RBAC aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="b2523-167">Use hello following steps tooenforce RBAC for different users:</span></span>

#### <a name="create-a-custom-role-definition-file-json"></a><span data-ttu-id="b2523-168">Bir özel rol tanımı dosyası (.json) oluşturun</span><span class="sxs-lookup"><span data-stu-id="b2523-168">Create a custom role definition file (.json)</span></span>

<span data-ttu-id="b2523-169">Merhaba, hangi kullanıcıların tooperform farklı eylemler kümesi örnek olay kılavuz rol tanımları verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b2523-169">hello following are sample Event Grid role definitions which allow users tooperform different sets of actions.</span></span>

<span data-ttu-id="b2523-170">**EventGridReadOnlyRole.json**: yalnızca okuma yalnızca işlemlerine izin verilir.</span><span class="sxs-lookup"><span data-stu-id="b2523-170">**EventGridReadOnlyRole.json**: Only allow read only operations.</span></span>
```json
{ 
  "Name": "Event grid read only role", 
  "Id": "7C0B6B59-A278-4B62-BA19-411B70753856", 
  "IsCustom": true, 
  "Description": "Event grid read only role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/read" 
  ], 
  "NotActions": [ 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription Id>" 
  ] 
}
```

<span data-ttu-id="b2523-171">**EventGridNoDeleteListKeysRole.json**: kısıtlı sonrası eylemler ancak silme işlemlerinin izin vermeyecek izin.</span><span class="sxs-lookup"><span data-stu-id="b2523-171">**EventGridNoDeleteListKeysRole.json**: Allow restricted post actions but disallow delete actions.</span></span>
```json
{ 
  "Name": "Event grid No Delete Listkeys role", 
  "Id": "B9170838-5F9D-4103-A1DE-60496F7C9174", 
  "IsCustom": true, 
  "Description": "Event grid No Delete Listkeys role", 
  "Actions": [     
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action" 
  ], 
  "NotActions": [ 
    "Microsoft.EventGrid/*/delete" 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription id>" 
  ] 
}
```
 
<span data-ttu-id="b2523-172">**EventGridContributorRole.json**: tüm olay kılavuz eylemleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="b2523-172">**EventGridContributorRole.json**: Allows all event grid actions.</span></span>  
```json
{ 
  "Name": "Event grid contributor role", 
  "Id": "4BA6FB33-2955-491B-A74F-53C9126C9514", 
  "IsCustom": true, 
  "Description": "Event grid contributor role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/*/delete", 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
  ], 
  "NotActions": [], 
  "AssignableScopes": [ 
    "/subscriptions/d48566a8-2428-4a6c-8347-9675d09fb851" 
  ] 
} 
```

#### <a name="install-and-login-tooazure-cli"></a><span data-ttu-id="b2523-173">Yükleme ve oturum açma tooAzure CLI</span><span class="sxs-lookup"><span data-stu-id="b2523-173">Install and login tooAzure CLI</span></span>

* <span data-ttu-id="b2523-174">Azure CLI Sürüm 0.8.8 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="b2523-174">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="b2523-175">tooinstall hello en son sürümünü ve ilişkilendirme Azure aboneliğinizle görmek [hello Azure CLI yükleyip](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="b2523-175">tooinstall hello latest version and associate it with your Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="b2523-176">Azure Resource Manager'da Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b2523-176">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="b2523-177">Çok Git[hello Resource Manager ile Azure CLI kullanarak hello](../xplat-cli-azure-resource-manager.md) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="b2523-177">Go too[Using hello Azure CLI with hello Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

#### <a name="create-a-custom-role"></a><span data-ttu-id="b2523-178">Özel bir rol oluşturun</span><span class="sxs-lookup"><span data-stu-id="b2523-178">Create a custom role</span></span>

<span data-ttu-id="b2523-179">toocreate özel bir rol kullanın:</span><span class="sxs-lookup"><span data-stu-id="b2523-179">toocreate a custom role, use:</span></span>

    azure role create --inputfile <file path>

#### <a name="assign-hello-role-tooa-user"></a><span data-ttu-id="b2523-180">Merhaba rol tooa kullanıcı atama</span><span class="sxs-lookup"><span data-stu-id="b2523-180">Assign hello role tooa user</span></span>


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a><span data-ttu-id="b2523-181">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b2523-181">Next steps</span></span>

* <span data-ttu-id="b2523-182">Bir giriş tooEvent kılavuz için bkz: [olay kılavuz hakkında](overview.md)</span><span class="sxs-lookup"><span data-stu-id="b2523-182">For an introduction tooEvent Grid, see [About Event Grid](overview.md)</span></span>
