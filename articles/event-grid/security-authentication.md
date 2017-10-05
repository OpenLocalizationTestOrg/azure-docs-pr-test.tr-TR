---
title: "Azure olay kılavuz güvenlik ve kimlik doğrulama"
description: "Azure olay kılavuz ve onun kavramlarını açıklar."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/14/2017
ms.author: babanisa
ms.openlocfilehash: b6e1c7587c0b47d04862b4850741aaa3b7d191a8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="event-grid-security-and-authentication"></a><span data-ttu-id="76672-103">Olay kılavuz güvenlik ve kimlik doğrulama</span><span class="sxs-lookup"><span data-stu-id="76672-103">Event Grid security and authentication</span></span> 

<span data-ttu-id="76672-104">Azure olay kılavuz üç tür kimlik doğrulama vardır:</span><span class="sxs-lookup"><span data-stu-id="76672-104">Azure Event Grid has three types of authentication:</span></span>

* <span data-ttu-id="76672-105">Olay abonelikleri</span><span class="sxs-lookup"><span data-stu-id="76672-105">Event subscriptions</span></span>
* <span data-ttu-id="76672-106">Olay yayımlama</span><span class="sxs-lookup"><span data-stu-id="76672-106">Event publishing</span></span>
* <span data-ttu-id="76672-107">Web kancası olay teslimi</span><span class="sxs-lookup"><span data-stu-id="76672-107">WebHook event delivery</span></span>

## <a name="webhook-event-delivery"></a><span data-ttu-id="76672-108">Web kancası olay teslimi</span><span class="sxs-lookup"><span data-stu-id="76672-108">WebHook Event delivery</span></span>

<span data-ttu-id="76672-109">Web kancası Azure olay kılavuz gelen gerçek zamanlı olaylarını almak için birçok yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="76672-109">Webhooks are one of many ways to receive events in real time from Azure Event Grid.</span></span>

<span data-ttu-id="76672-110">Olduğundan her zaman yeni bir olay teslim edilecek hazır, olay kılavuz olay gövdesine sahip, bir Web kancası olan HTTP isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="76672-110">Every time there is a new event ready to be delivered, Event Grid sends an HTTP request with to your WebHook with the event in the body.</span></span>

<span data-ttu-id="76672-111">Kendi Web kancası bitiş noktası içeren olay kılavuz kaydettiğinizde, uç nokta sahipliği kanıtlamak için basit bir doğrulama kodu içeren bir POST isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="76672-111">When you register your own WebHook endpoint with Event Grid, it sends you a POST request with a simple validation code in order to prove endpoint ownership.</span></span> <span data-ttu-id="76672-112">Uygulamanızın geri doğrulama kodu Yankı tarafından yanıt vermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="76672-112">Your app needs to respond by echoing back the validation code.</span></span> <span data-ttu-id="76672-113">Olay kılavuz olayları doğrulama geçmedi Web kancası Uç noktalara teslim değil.</span><span class="sxs-lookup"><span data-stu-id="76672-113">Event Grid will not deliver events to WebHook endpoints that have not passed the validation.</span></span>
 
### <a name="validation-details"></a><span data-ttu-id="76672-114">Doğrulama ayrıntıları:</span><span class="sxs-lookup"><span data-stu-id="76672-114">Validation details:</span></span>

* <span data-ttu-id="76672-115">Olay aboneliği oluşturma/güncelleştirme zaman olay kılavuz "SubscriptionValidationEvent" olay hedef uç noktasına gönderir.</span><span class="sxs-lookup"><span data-stu-id="76672-115">At the time of event subscription creation/update, Event Grid posts a “SubscriptionValidationEvent” event to the target endpoint.</span></span>
* <span data-ttu-id="76672-116">Olay bir üstbilgi değeri "Olay türü: doğrulama" içerir.</span><span class="sxs-lookup"><span data-stu-id="76672-116">The event contains a header value “Event-Type: Validation”.</span></span>
* <span data-ttu-id="76672-117">Olay gövdesi diğer olay kılavuz olaylarla aynı şeması vardır.</span><span class="sxs-lookup"><span data-stu-id="76672-117">The event body has the same schema as other Event Grid events.</span></span>
* <span data-ttu-id="76672-118">Olay verileri rastgele oluşturulmuş bir dize "ValidationCode" özelliğiyle örneğin içerir "ValidationCode: acb13...".</span><span class="sxs-lookup"><span data-stu-id="76672-118">The event data includes a “ValidationCode” property with a randomly generated string e.g. “ValidationCode: acb13…”.</span></span>

<span data-ttu-id="76672-119">Uç nokta sahipliği kanıtlamak için geri doğrulama kodu örneğin echo "ValidationResponse: acb13...".</span><span class="sxs-lookup"><span data-stu-id="76672-119">In order to prove endpoint ownership, echo back the validation code e.g “ValidationResponse: acb13…”.</span></span>

<span data-ttu-id="76672-120">Son olarak, Azure olay kılavuz yalnızca HTTPS Web kancası uç noktaları desteklediğini dikkate almak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="76672-120">Finally, it is important to note that Azure Event Grid only supports HTTPS webhook endpoints.</span></span>
## <a name="event-subscription"></a><span data-ttu-id="76672-121">Olay aboneliği</span><span class="sxs-lookup"><span data-stu-id="76672-121">Event subscription</span></span>

<span data-ttu-id="76672-122">Bir olaya abone olmak için bilmeniz gereken **Microsoft.EventGrid/EventSubscriptions/Write** gerekli kaynak izni.</span><span class="sxs-lookup"><span data-stu-id="76672-122">To subscribe to an event, you must have the **Microsoft.EventGrid/EventSubscriptions/Write** permission on the required resource.</span></span> <span data-ttu-id="76672-123">Kapsamındaki yeni bir abonelik kaynağının yazmak için bu izni gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="76672-123">You need this permission because you are writing a new subscription at the scope of the resource.</span></span> <span data-ttu-id="76672-124">Gerekli kaynak sistem konusunu ya da özel konu abone göre farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="76672-124">The required resource differs based on whether you are subscribing to a system topic or custom topic.</span></span> <span data-ttu-id="76672-125">Her iki tür, bu bölümde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="76672-125">Both types are described in this section.</span></span>

### <a name="system-topics-azure-service-publishers"></a><span data-ttu-id="76672-126">Sistem konuları (Azure hizmeti yayımcılar)</span><span class="sxs-lookup"><span data-stu-id="76672-126">System topics (Azure service publishers)</span></span>

<span data-ttu-id="76672-127">Sistem konuları için yeni bir olay aboneliği kapsamında olay yayımlama kaynağının yazma izni gerekir.</span><span class="sxs-lookup"><span data-stu-id="76672-127">For system topics, you need permission to write a new event subscription at the scope of the resource publishing the event.</span></span> <span data-ttu-id="76672-128">Kaynak biçimi şöyledir:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span><span class="sxs-lookup"><span data-stu-id="76672-128">The format of the resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span></span>

<span data-ttu-id="76672-129">Örneğin, bir depolama hesabı üzerinde bir olaya abone olmak için adlı **myacct**, üzerinde Microsoft.EventGrid/EventSubscriptions/Write izniniz olmalıdır:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span><span class="sxs-lookup"><span data-stu-id="76672-129">For example, to subscribe to an event on a storage account named **myacct**, you need the Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span></span>

### <a name="custom-topics"></a><span data-ttu-id="76672-130">Özel konular</span><span class="sxs-lookup"><span data-stu-id="76672-130">Custom topics</span></span>

<span data-ttu-id="76672-131">Özel konular için yeni bir olay aboneliği kapsamında olay kılavuz konunun yazma izni gerekir.</span><span class="sxs-lookup"><span data-stu-id="76672-131">For custom topics, you need permission to write a new event subscription at the scope of the Event Grid topic.</span></span> <span data-ttu-id="76672-132">Kaynak biçimi şöyledir:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span><span class="sxs-lookup"><span data-stu-id="76672-132">The format of the resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span></span>

<span data-ttu-id="76672-133">Örneğin, özel bir konuya abone olmak için adlı **mytopic**, üzerinde Microsoft.EventGrid/EventSubscriptions/Write izniniz olmalıdır:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span><span class="sxs-lookup"><span data-stu-id="76672-133">For example, to subscribe to a custom topic named **mytopic**, you need the Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span></span>

## <a name="topic-publishing"></a><span data-ttu-id="76672-134">Konu yayımlama</span><span class="sxs-lookup"><span data-stu-id="76672-134">Topic publishing</span></span>

<span data-ttu-id="76672-135">Konular, paylaşılan erişim imzası (SAS) veya anahtar kimlik doğrulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="76672-135">Topics use either Shared Access Signature (SAS) or key authentication.</span></span> <span data-ttu-id="76672-136">SAS öneririz, ancak anahtar kimlik doğrulaması basit programlama sağlar ve birçok varolan Web kancası yayımcıları ile uyumludur.</span><span class="sxs-lookup"><span data-stu-id="76672-136">We recommend SAS, but key authentication provides simple programming, and is compatible with many existing webhook publishers.</span></span> 

<span data-ttu-id="76672-137">HTTP üstbilgisinde kimlik doğrulama değeri içerir.</span><span class="sxs-lookup"><span data-stu-id="76672-137">You include the authentication value in the HTTP header.</span></span> <span data-ttu-id="76672-138">SA'ları için kullanmak **aeg sas belirteci** üstbilgi değeri.</span><span class="sxs-lookup"><span data-stu-id="76672-138">For SAS, use **aeg-sas-token** for the header value.</span></span> <span data-ttu-id="76672-139">Anahtar kimlik doğrulaması için kullanmak **aeg sas anahtarı** üstbilgi değeri.</span><span class="sxs-lookup"><span data-stu-id="76672-139">For key authentication, use **aeg-sas-key** for the header value.</span></span>

### <a name="key-authentication"></a><span data-ttu-id="76672-140">Anahtar kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="76672-140">Key authentication</span></span>

<span data-ttu-id="76672-141">Anahtar kimlik doğrulaması kimlik doğrulaması en basit biçimidir.</span><span class="sxs-lookup"><span data-stu-id="76672-141">Key authentication is the simplest form of authentication.</span></span> <span data-ttu-id="76672-142">Biçimi kullanın:`aeg-sas-key: <your key>`</span><span class="sxs-lookup"><span data-stu-id="76672-142">Use the format: `aeg-sas-key: <your key>`</span></span>

<span data-ttu-id="76672-143">Örneğin, bir anahtar ile geçirin:</span><span class="sxs-lookup"><span data-stu-id="76672-143">For example, you pass a key with:</span></span> 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a><span data-ttu-id="76672-144">SAS belirteçleri</span><span class="sxs-lookup"><span data-stu-id="76672-144">SAS tokens</span></span>

<span data-ttu-id="76672-145">Olay kılavuz için SAS belirteci kaynağı, sona erme süresi ve imza içerir.</span><span class="sxs-lookup"><span data-stu-id="76672-145">SAS tokens for Event Grid include the resource, an expiration time, and a signature.</span></span> <span data-ttu-id="76672-146">SAS belirteci biçimi: `r={resource}&e={expiration}&s={signature}`.</span><span class="sxs-lookup"><span data-stu-id="76672-146">The format of the SAS token is: `r={resource}&e={expiration}&s={signature}`.</span></span>

<span data-ttu-id="76672-147">Kaynak olayların gönderilmesi konu yolu değil.</span><span class="sxs-lookup"><span data-stu-id="76672-147">The resource is the path for the topic to which you are sending events.</span></span> <span data-ttu-id="76672-148">Örneğin, geçerli bir kaynak yolu şöyledir:`https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span><span class="sxs-lookup"><span data-stu-id="76672-148">For example, a valid resource path is: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span></span>

<span data-ttu-id="76672-149">İmza bir anahtarı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="76672-149">You generate the signature from a key.</span></span>

<span data-ttu-id="76672-150">Örneğin, geçerli **aeg sas belirteci** değer:</span><span class="sxs-lookup"><span data-stu-id="76672-150">For example, a valid **aeg-sas-token** value is:</span></span>

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

<span data-ttu-id="76672-151">Aşağıdaki örnek, olay kılavuz ile kullanmak için bir SAS belirteci oluşturur:</span><span class="sxs-lookup"><span data-stu-id="76672-151">The following example creates a SAS token for use with Event Grid:</span></span>

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

## <a name="management-access-control"></a><span data-ttu-id="76672-152">Yönetim erişim denetimi</span><span class="sxs-lookup"><span data-stu-id="76672-152">Management Access Control</span></span>

<span data-ttu-id="76672-153">Azure olay kılavuz listesi olay abonelikleri gibi çeşitli yönetim işlemlerini yapmak için yeni kampanya oluşturmak ve anahtarlar oluşturmak için farklı kullanıcılara verilen erişim düzeyini denetlemenize olanak verir.</span><span class="sxs-lookup"><span data-stu-id="76672-153">Azure Event Grid allows you to control the level of access given to different users to do various management operations such as list event subscriptions, create new ones, and generate keys.</span></span> <span data-ttu-id="76672-154">Bu olay kılavuz Azure'nın rol tabanlı erişim denetleyin (RBAC) kullanır.</span><span class="sxs-lookup"><span data-stu-id="76672-154">Event Grid utilizes Azure's Role Based Access Check (RBAC) for this.</span></span>

### <a name="operation-types"></a><span data-ttu-id="76672-155">İşlem türleri</span><span class="sxs-lookup"><span data-stu-id="76672-155">Operation types</span></span>

<span data-ttu-id="76672-156">Azure olay kılavuz, aşağıdaki eylemleri destekler:</span><span class="sxs-lookup"><span data-stu-id="76672-156">Azure event grid supports the following actions:</span></span>

* <span data-ttu-id="76672-157">Microsoft.EventGrid/*/read</span><span class="sxs-lookup"><span data-stu-id="76672-157">Microsoft.EventGrid/*/read</span></span> 
* <span data-ttu-id="76672-158">Microsoft.EventGrid/*/write</span><span class="sxs-lookup"><span data-stu-id="76672-158">Microsoft.EventGrid/*/write</span></span> 
* <span data-ttu-id="76672-159">Microsoft.EventGrid/*/delete</span><span class="sxs-lookup"><span data-stu-id="76672-159">Microsoft.EventGrid/*/delete</span></span> 
* <span data-ttu-id="76672-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span><span class="sxs-lookup"><span data-stu-id="76672-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span></span> 
* <span data-ttu-id="76672-161">Microsoft.EventGrid/topics/listKeys/action</span><span class="sxs-lookup"><span data-stu-id="76672-161">Microsoft.EventGrid/topics/listKeys/action</span></span> 
* <span data-ttu-id="76672-162">Microsoft.EventGrid/topics/regenerateKey/action</span><span class="sxs-lookup"><span data-stu-id="76672-162">Microsoft.EventGrid/topics/regenerateKey/action</span></span>

<span data-ttu-id="76672-163">Son üç işlemi normal okuma işlemleri dışında filtrelenmiş potansiyel olarak gizli bilgileri döndürün.</span><span class="sxs-lookup"><span data-stu-id="76672-163">The last three operations return potentially secret information which gets filtered out of normal read operations.</span></span> <span data-ttu-id="76672-164">Bu, bu işlemler için erişimi kısıtlamak en iyi uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="76672-164">It is best practice for you to restrict access to these operations.</span></span> <span data-ttu-id="76672-165">Özel roller kullanılarak oluşturulabilir [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure komut satırı arabirimi (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md)ve [REST API](../active-directory/role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="76672-165">Custom roles can be created using [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md), and the [REST API](../active-directory/role-based-access-control-manage-access-rest.md).</span></span>

### <a name="enforcing-role-based-access-check-rbac"></a><span data-ttu-id="76672-166">Rol uygulamaya dayalı erişim denetimi (RBAC)</span><span class="sxs-lookup"><span data-stu-id="76672-166">Enforcing Role Based Access Check (RBAC)</span></span>

<span data-ttu-id="76672-167">Farklı kullanıcılar için RBAC zorlamak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="76672-167">Use the following steps to enforce RBAC for different users:</span></span>

#### <a name="create-a-custom-role-definition-file-json"></a><span data-ttu-id="76672-168">Bir özel rol tanımı dosyası (.json) oluşturun</span><span class="sxs-lookup"><span data-stu-id="76672-168">Create a custom role definition file (.json)</span></span>

<span data-ttu-id="76672-169">Kullanıcıların farklı eylemler gerçekleştirmesine olanak sağlayan örnek olay kılavuz rol tanımları verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="76672-169">The following are sample Event Grid role definitions which allow users to perform different sets of actions.</span></span>

<span data-ttu-id="76672-170">**EventGridReadOnlyRole.json**: yalnızca okuma yalnızca işlemlerine izin verilir.</span><span class="sxs-lookup"><span data-stu-id="76672-170">**EventGridReadOnlyRole.json**: Only allow read only operations.</span></span>
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

<span data-ttu-id="76672-171">**EventGridNoDeleteListKeysRole.json**: kısıtlı sonrası eylemler ancak silme işlemlerinin izin vermeyecek izin.</span><span class="sxs-lookup"><span data-stu-id="76672-171">**EventGridNoDeleteListKeysRole.json**: Allow restricted post actions but disallow delete actions.</span></span>
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
 
<span data-ttu-id="76672-172">**EventGridContributorRole.json**: tüm olay kılavuz eylemleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="76672-172">**EventGridContributorRole.json**: Allows all event grid actions.</span></span>  
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

#### <a name="install-and-login-to-azure-cli"></a><span data-ttu-id="76672-173">Yükleme ve Azure CLI için oturum açma</span><span class="sxs-lookup"><span data-stu-id="76672-173">Install and login to Azure CLI</span></span>

* <span data-ttu-id="76672-174">Azure CLI Sürüm 0.8.8 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="76672-174">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="76672-175">En son sürümünü yükleyin ve Azure aboneliğinizle ilişkilendirmek için bkz: [Azure CLI'yi yükleme ve yapılandırma](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="76672-175">To install the latest version and associate it with your Azure subscription, see [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="76672-176">Azure Resource Manager'da Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="76672-176">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="76672-177">Git [Resource Manager ile Azure CLI kullanarak](../xplat-cli-azure-resource-manager.md) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="76672-177">Go to [Using the Azure CLI with the Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

#### <a name="create-a-custom-role"></a><span data-ttu-id="76672-178">Özel bir rol oluşturun</span><span class="sxs-lookup"><span data-stu-id="76672-178">Create a custom role</span></span>

<span data-ttu-id="76672-179">Özel bir rol oluşturmak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="76672-179">To create a custom role, use:</span></span>

    azure role create --inputfile <file path>

#### <a name="assign-the-role-to-a-user"></a><span data-ttu-id="76672-180">Bir kullanıcıya rol atama</span><span class="sxs-lookup"><span data-stu-id="76672-180">Assign the role to a user</span></span>


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a><span data-ttu-id="76672-181">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="76672-181">Next steps</span></span>

* <span data-ttu-id="76672-182">Olay kılavuz giriş için bkz: [olay kılavuz hakkında](overview.md)</span><span class="sxs-lookup"><span data-stu-id="76672-182">For an introduction to Event Grid, see [About Event Grid](overview.md)</span></span>
