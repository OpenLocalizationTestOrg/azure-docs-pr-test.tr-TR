---
title: "aaaAzure Resource Manager istek sınırlarını | Microsoft Docs"
description: "Abonelik sınırları erişildiğinde Azure Resource Manager ile azaltma toouse nasıl istekleri açıklar."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: e1047233-b8e4-4232-8919-3268d93a3824
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: ea274f3145af36aac753730e1f280d8a8b59c3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-resource-manager-requests"></a><span data-ttu-id="92dfd-103">Resource Manager istekleri azaltma</span><span class="sxs-lookup"><span data-stu-id="92dfd-103">Throttling Resource Manager requests</span></span>
<span data-ttu-id="92dfd-104">Her abonelik ve Kiracı, Resource Manager sınırları istekleri too15, saat başına 000 okuma ve istekleri too1, saat başına 200 yazma.</span><span class="sxs-lookup"><span data-stu-id="92dfd-104">For each subscription and tenant, Resource Manager limits read requests too15,000 per hour and write requests too1,200 per hour.</span></span> <span data-ttu-id="92dfd-105">Bu sınırlar tooeach Azure Resource Manager örneğinin geçerli; Her Azure bölgesi birden çok örneği vardır ve Azure Resource Manager olduğu dağıtılan tooall Azure bölgeleri.</span><span class="sxs-lookup"><span data-stu-id="92dfd-105">These limits apply tooeach Azure Resource Manager instance; there are multiple instances in every Azure region, and Azure Resource Manager is deployed tooall Azure regions.</span></span>  <span data-ttu-id="92dfd-106">Sınırları pratikte, yukarıda listelenen daha etkili bir şekilde çok daha yüksek olacak şekilde bir kullanıcı olarak istekleri genellikle birçok farklı örnekleri tarafından sunulur.</span><span class="sxs-lookup"><span data-stu-id="92dfd-106">So, in practice, limits are effectively much higher than those listed above, as user requests are generally serviced by many different instances.</span></span>

<span data-ttu-id="92dfd-107">Uygulama veya betik bu sınırları ulaşırsa, isteklerinizi toothrottle gerekir.</span><span class="sxs-lookup"><span data-stu-id="92dfd-107">If your application or script reaches these limits, you need toothrottle your requests.</span></span> <span data-ttu-id="92dfd-108">Bu konuda sahip hello sınırı ulaşmadan önce kalan toodetermine hello istekleri nasıl ve ne gösterilmektedir hello sınıra ulaştığınızda toorespond.</span><span class="sxs-lookup"><span data-stu-id="92dfd-108">This topic shows you how toodetermine hello remaining requests you have before reaching hello limit, and how toorespond when you have reached hello limit.</span></span>

<span data-ttu-id="92dfd-109">Merhaba sınırına ulaştığında, hello HTTP durum kodu alırsınız **429 çok fazla istek**.</span><span class="sxs-lookup"><span data-stu-id="92dfd-109">When you reach hello limit, you receive hello HTTP status code **429 Too many requests**.</span></span>

<span data-ttu-id="92dfd-110">Merhaba istek sayısı aboneliğinizi veya Kiracı kapsamlı tooeither değil.</span><span class="sxs-lookup"><span data-stu-id="92dfd-110">hello number of requests is scoped tooeither your subscription or your tenant.</span></span> <span data-ttu-id="92dfd-111">Eş zamanlı uygulamaları, aboneliğinizde istekleri yapan birden çok varsa, bu uygulamalardan hello istekler toodetermine hello kalan istek sayısı birlikte eklenir.</span><span class="sxs-lookup"><span data-stu-id="92dfd-111">If you have multiple, concurrent applications making requests in your subscription, hello requests from those applications are added together toodetermine hello number of remaining requests.</span></span>

<span data-ttu-id="92dfd-112">Kapsamlı abonelik olanları hello içeren hello kaynak grupları, aboneliğinizdeki alma gibi abonelik kimliğinizi geçirme isteklerdir.</span><span class="sxs-lookup"><span data-stu-id="92dfd-112">Subscription scoped requests are ones hello involve passing your subscription id, such as retrieving hello resource groups in your subscription.</span></span> <span data-ttu-id="92dfd-113">Kapsamlı Kiracı isteklerini alma geçerli Azure konumları gibi abonelik kimliğinizi dahil etmeyin.</span><span class="sxs-lookup"><span data-stu-id="92dfd-113">Tenant scoped requests do not include your subscription id, such as retrieving valid Azure locations.</span></span>

## <a name="remaining-requests"></a><span data-ttu-id="92dfd-114">Kalan istekleri</span><span class="sxs-lookup"><span data-stu-id="92dfd-114">Remaining requests</span></span>
<span data-ttu-id="92dfd-115">Yanıt Üstbilgileri inceleyerek kalan istekleri hello sayısını belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92dfd-115">You can determine hello number of remaining requests by examining response headers.</span></span> <span data-ttu-id="92dfd-116">Her istek hello numarasının kalan okuma ve yazma isteklerini değerlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="92dfd-116">Each request includes values for hello number of remaining read and write requests.</span></span> <span data-ttu-id="92dfd-117">Merhaba aşağıdaki tabloda bu değerleri inceleyebilirsiniz hello yanıt üstbilgilerini açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="92dfd-117">hello following table describes hello response headers you can examine for those values:</span></span>

| <span data-ttu-id="92dfd-118">Yanıt üst bilgisi</span><span class="sxs-lookup"><span data-stu-id="92dfd-118">Response header</span></span> | <span data-ttu-id="92dfd-119">Açıklama</span><span class="sxs-lookup"><span data-stu-id="92dfd-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="92dfd-120">x-MS-ratelimit-Remaining-Subscription-Reads</span><span class="sxs-lookup"><span data-stu-id="92dfd-120">x-ms-ratelimit-remaining-subscription-reads</span></span> |<span data-ttu-id="92dfd-121">Kalan abonelik kapsamlı okur</span><span class="sxs-lookup"><span data-stu-id="92dfd-121">Subscription scoped reads remaining</span></span> |
| <span data-ttu-id="92dfd-122">x-MS-ratelimit-Remaining-Subscription-Writes</span><span class="sxs-lookup"><span data-stu-id="92dfd-122">x-ms-ratelimit-remaining-subscription-writes</span></span> |<span data-ttu-id="92dfd-123">Kalan abonelik kapsamlı Yazar</span><span class="sxs-lookup"><span data-stu-id="92dfd-123">Subscription scoped writes remaining</span></span> |
| <span data-ttu-id="92dfd-124">x-MS-ratelimit-Remaining-tenant-Reads</span><span class="sxs-lookup"><span data-stu-id="92dfd-124">x-ms-ratelimit-remaining-tenant-reads</span></span> |<span data-ttu-id="92dfd-125">Kalan kapsamlı kiracı okur</span><span class="sxs-lookup"><span data-stu-id="92dfd-125">Tenant scoped reads remaining</span></span> |
| <span data-ttu-id="92dfd-126">x-MS-ratelimit-Remaining-tenant-Writes</span><span class="sxs-lookup"><span data-stu-id="92dfd-126">x-ms-ratelimit-remaining-tenant-writes</span></span> |<span data-ttu-id="92dfd-127">Kalan kapsamlı Kiracı Yazar</span><span class="sxs-lookup"><span data-stu-id="92dfd-127">Tenant scoped writes remaining</span></span> |
| <span data-ttu-id="92dfd-128">x-MS-ratelimit-Remaining-Subscription-Resource-Requests</span><span class="sxs-lookup"><span data-stu-id="92dfd-128">x-ms-ratelimit-remaining-subscription-resource-requests</span></span> |<span data-ttu-id="92dfd-129">Abonelik, kaynak türü istekleri kalan kapsamlı.</span><span class="sxs-lookup"><span data-stu-id="92dfd-129">Subscription scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="92dfd-130">Bu üstbilgi değerini yalnızca bir hizmet hello varsayılan sınır kılınmış döndürülür.</span><span class="sxs-lookup"><span data-stu-id="92dfd-130">This header value is only returned if a service has overridden hello default limit.</span></span> <span data-ttu-id="92dfd-131">Resource Manager hello abonelik okuma veya yazmaları yerine bu değer ekler.</span><span class="sxs-lookup"><span data-stu-id="92dfd-131">Resource Manager adds this value instead of hello subscription reads or writes.</span></span> |
| <span data-ttu-id="92dfd-132">x-MS-ratelimit-Remaining-Subscription-Resource-entities-Read</span><span class="sxs-lookup"><span data-stu-id="92dfd-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span></span> |<span data-ttu-id="92dfd-133">Abonelik, kaynak türü koleksiyonu isteklerini kalan kapsamlı.</span><span class="sxs-lookup"><span data-stu-id="92dfd-133">Subscription scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="92dfd-134">Bu üstbilgi değerini yalnızca bir hizmet hello varsayılan sınır kılınmış döndürülür.</span><span class="sxs-lookup"><span data-stu-id="92dfd-134">This header value is only returned if a service has overridden hello default limit.</span></span> <span data-ttu-id="92dfd-135">Bu değer kalan koleksiyonu isteklerini (liste kaynakları) hello sayısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="92dfd-135">This value provides hello number of remaining collection requests (list resources).</span></span> |
| <span data-ttu-id="92dfd-136">x-MS-ratelimit-Remaining-tenant-Resource-Requests</span><span class="sxs-lookup"><span data-stu-id="92dfd-136">x-ms-ratelimit-remaining-tenant-resource-requests</span></span> |<span data-ttu-id="92dfd-137">Kiracı kaynak türü istekleri kalan kapsamlı.</span><span class="sxs-lookup"><span data-stu-id="92dfd-137">Tenant scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="92dfd-138">Bu üst yalnızca Kiracı düzeyinde istekleri için eklenir ve yalnızca bir hizmet hello varsayılan sınır geçersiz kılınmış.</span><span class="sxs-lookup"><span data-stu-id="92dfd-138">This header is only added for requests at tenant level, and only if a service has overridden hello default limit.</span></span> <span data-ttu-id="92dfd-139">Resource Manager hello Kiracı okuma veya yazmaları yerine bu değer ekler.</span><span class="sxs-lookup"><span data-stu-id="92dfd-139">Resource Manager adds this value instead of hello tenant reads or writes.</span></span> |
| <span data-ttu-id="92dfd-140">x-MS-ratelimit-Remaining-tenant-Resource-entities-Read</span><span class="sxs-lookup"><span data-stu-id="92dfd-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span></span> |<span data-ttu-id="92dfd-141">Kiracı kaynak türü koleksiyonu isteklerini kalan kapsamlı.</span><span class="sxs-lookup"><span data-stu-id="92dfd-141">Tenant scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="92dfd-142">Bu üst yalnızca Kiracı düzeyinde istekleri için eklenir ve yalnızca bir hizmet hello varsayılan sınır geçersiz kılınmış.</span><span class="sxs-lookup"><span data-stu-id="92dfd-142">This header is only added for requests at tenant level, and only if a service has overridden hello default limit.</span></span> |

## <a name="retrieving-hello-header-values"></a><span data-ttu-id="92dfd-143">Merhaba üstbilgi değerlerini alma</span><span class="sxs-lookup"><span data-stu-id="92dfd-143">Retrieving hello header values</span></span>
<span data-ttu-id="92dfd-144">Kod ya da komut dosyasında bu üstbilgi değerlerini alma herhangi bir üstbilgi değeri almaktan farklı değildir.</span><span class="sxs-lookup"><span data-stu-id="92dfd-144">Retrieving these header values in your code or script is no different than retrieving any header value.</span></span> 

<span data-ttu-id="92dfd-145">Örneğin, **C#**, hello üstbilgi değeri almak bir **HttpWebResponse** adlı nesne **yanıt** koddan hello ile:</span><span class="sxs-lookup"><span data-stu-id="92dfd-145">For example, in **C#**, you retrieve hello header value from an **HttpWebResponse** object named **response** with hello following code:</span></span>

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

<span data-ttu-id="92dfd-146">İçinde **PowerShell**, bir Invoke-WebRequest işlemden hello üstbilgi değeri alır.</span><span class="sxs-lookup"><span data-stu-id="92dfd-146">In **PowerShell**, you retrieve hello header value from an Invoke-WebRequest operation.</span></span>

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

<span data-ttu-id="92dfd-147">Veya, toosee hello kalan istekleri hata ayıklama için hello sağlayabilir istiyorsanız **-Debug** parametresi, **PowerShell** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="92dfd-147">Or, if want toosee hello remaining requests for debugging, you can provide hello **-Debug** parameter on your **PowerShell** cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -Debug
```

<span data-ttu-id="92dfd-148">Aşağıdaki yanıt değeri hello dahil olmak üzere birden fazla değer döndüren:</span><span class="sxs-lookup"><span data-stu-id="92dfd-148">Which returns many values, including hello following response value:</span></span>

```powershell
...
DEBUG: ============================ HTTP RESPONSE ============================

Status Code:
OK

Headers:
Pragma                        : no-cache
x-ms-ratelimit-remaining-subscription-reads: 14999
...
```

<span data-ttu-id="92dfd-149">İçinde **Azure CLI**, kullanarak hello üstbilgi değeri almak hello daha ayrıntılı seçeneği.</span><span class="sxs-lookup"><span data-stu-id="92dfd-149">In **Azure CLI**, you retrieve hello header value by using hello more verbose option.</span></span>

```azurecli
azure group list -vv --json
```

<span data-ttu-id="92dfd-150">Hangi nesne aşağıdaki hello dahil olmak üzere birçok değerleri döndürür:</span><span class="sxs-lookup"><span data-stu-id="92dfd-150">Which returns many values, including hello following object:</span></span>

```azurecli
...
silly: returnObject
{
  "statusCode": 200,
  "header": {
    "cache-control": "no-cache",
    "pragma": "no-cache",
    "content-type": "application/json; charset=utf-8",
    "expires": "-1",
    "x-ms-ratelimit-remaining-subscription-reads": "14998",
    ...
```

## <a name="waiting-before-sending-next-request"></a><span data-ttu-id="92dfd-151">Sonraki istek gönderilmeden önce bekleniyor</span><span class="sxs-lookup"><span data-stu-id="92dfd-151">Waiting before sending next request</span></span>
<span data-ttu-id="92dfd-152">Merhaba istek sınırına ulaştığında, Resource Manager hello döndürür **429** HTTP durum kodu ve **yeniden deneme sonrasında** hello üstbilgi değeri.</span><span class="sxs-lookup"><span data-stu-id="92dfd-152">When you reach hello request limit, Resource Manager returns hello **429** HTTP status code and a **Retry-After** value in hello header.</span></span> <span data-ttu-id="92dfd-153">Merhaba **yeniden deneme sonrasında** değeri hello sonraki istek gönderilmeden önce uygulamanız beklemesi gereken saniye (veya uyku) hello sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="92dfd-153">hello **Retry-After** value specifies hello number of seconds your application should wait (or sleep) before sending hello next request.</span></span> <span data-ttu-id="92dfd-154">Merhaba yeniden deneme değeri geçmeden önce bir isteği gönderirseniz, isteğiniz işlenmedi ve yeni bir yeniden deneme değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="92dfd-154">If you send a request before hello retry value has elapsed, your request is not processed and a new retry value is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92dfd-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="92dfd-155">Next steps</span></span>

* <span data-ttu-id="92dfd-156">Sınırları ve kotalar hakkında daha fazla bilgi için bkz: [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="92dfd-156">For more information about limits and quotas, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>
* <span data-ttu-id="92dfd-157">zaman uyumsuz REST istekleri işleme hakkında toolearn bkz [izlemek zaman uyumsuz Azure işlemleri](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="92dfd-157">toolearn about handling asynchronous REST requests, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
