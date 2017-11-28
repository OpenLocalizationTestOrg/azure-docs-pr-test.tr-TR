---
title: "Azure Resource Manager istek sınırlarını | Microsoft Docs"
description: "Abonelik sınırları erişildiğinde Azure Resource Manager istekleriyle azaltma kullanmayı açıklar."
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
ms.openlocfilehash: 6d7eeaf460674c3ab98425a5412ffa465b9ffd1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="throttling-resource-manager-requests"></a><span data-ttu-id="11b4b-103">Resource Manager istekleri azaltma</span><span class="sxs-lookup"><span data-stu-id="11b4b-103">Throttling Resource Manager requests</span></span>
<span data-ttu-id="11b4b-104">Her abonelik ve Kiracı, Resource Manager sınırları saatte 15.000 isteklerine okuma ve yazma isteklerinin saatte 1.200 için.</span><span class="sxs-lookup"><span data-stu-id="11b4b-104">For each subscription and tenant, Resource Manager limits read requests to 15,000 per hour and write requests to 1,200 per hour.</span></span> <span data-ttu-id="11b4b-105">Bu sınırlar her Azure Resource Manager örnek için geçerli olur; Her Azure bölgesi birden çok örneği vardır ve Azure Resource Manager için tüm Azure bölgeleri dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="11b4b-105">These limits apply to each Azure Resource Manager instance; there are multiple instances in every Azure region, and Azure Resource Manager is deployed to all Azure regions.</span></span>  <span data-ttu-id="11b4b-106">Sınırları pratikte, yukarıda listelenen daha etkili bir şekilde çok daha yüksek olacak şekilde bir kullanıcı olarak istekleri genellikle birçok farklı örnekleri tarafından sunulur.</span><span class="sxs-lookup"><span data-stu-id="11b4b-106">So, in practice, limits are effectively much higher than those listed above, as user requests are generally serviced by many different instances.</span></span>

<span data-ttu-id="11b4b-107">Uygulama veya betik bu sınırları ulaşırsa, istek kısıtlama gerekir.</span><span class="sxs-lookup"><span data-stu-id="11b4b-107">If your application or script reaches these limits, you need to throttle your requests.</span></span> <span data-ttu-id="11b4b-108">Bu konuda, sınır ulaşmadan sahip kalan istekleri belirleme ve nasıl sınıra ulaştığınızda yanıt gösterir.</span><span class="sxs-lookup"><span data-stu-id="11b4b-108">This topic shows you how to determine the remaining requests you have before reaching the limit, and how to respond when you have reached the limit.</span></span>

<span data-ttu-id="11b4b-109">Sınırına ulaştığında, HTTP durum kodunu alma **429 çok fazla istek**.</span><span class="sxs-lookup"><span data-stu-id="11b4b-109">When you reach the limit, you receive the HTTP status code **429 Too many requests**.</span></span>

<span data-ttu-id="11b4b-110">İstek sayısı aboneliğiniz ya da Kiracı kapsamlıdır.</span><span class="sxs-lookup"><span data-stu-id="11b4b-110">The number of requests is scoped to either your subscription or your tenant.</span></span> <span data-ttu-id="11b4b-111">Birden çok varsa, aboneliğinizde istekleri yapan eşzamanlı uygulamalar bu uygulamalardan istekler eklenir birlikte kalan isteklerinin sayısını belirlemek için.</span><span class="sxs-lookup"><span data-stu-id="11b4b-111">If you have multiple, concurrent applications making requests in your subscription, the requests from those applications are added together to determine the number of remaining requests.</span></span>

<span data-ttu-id="11b4b-112">Abonelik kapsamlı olanları aboneliğinizde kaynak alma gibi abonelik kimliğinizi geçirme involve gruplar isteklerdir.</span><span class="sxs-lookup"><span data-stu-id="11b4b-112">Subscription scoped requests are ones the involve passing your subscription id, such as retrieving the resource groups in your subscription.</span></span> <span data-ttu-id="11b4b-113">Kapsamlı Kiracı isteklerini alma geçerli Azure konumları gibi abonelik kimliğinizi dahil etmeyin.</span><span class="sxs-lookup"><span data-stu-id="11b4b-113">Tenant scoped requests do not include your subscription id, such as retrieving valid Azure locations.</span></span>

## <a name="remaining-requests"></a><span data-ttu-id="11b4b-114">Kalan istekleri</span><span class="sxs-lookup"><span data-stu-id="11b4b-114">Remaining requests</span></span>
<span data-ttu-id="11b4b-115">Yanıt Üstbilgileri inceleyerek kalan istek sayısını belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11b4b-115">You can determine the number of remaining requests by examining response headers.</span></span> <span data-ttu-id="11b4b-116">Her istek için kalan okuma ve yazma isteklerinin sayısı değerlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="11b4b-116">Each request includes values for the number of remaining read and write requests.</span></span> <span data-ttu-id="11b4b-117">Aşağıdaki tabloda, bu değerleri inceleyebilirsiniz yanıt üstbilgilerini açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="11b4b-117">The following table describes the response headers you can examine for those values:</span></span>

| <span data-ttu-id="11b4b-118">Yanıt üst bilgisi</span><span class="sxs-lookup"><span data-stu-id="11b4b-118">Response header</span></span> | <span data-ttu-id="11b4b-119">Açıklama</span><span class="sxs-lookup"><span data-stu-id="11b4b-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="11b4b-120">x-MS-ratelimit-Remaining-Subscription-Reads</span><span class="sxs-lookup"><span data-stu-id="11b4b-120">x-ms-ratelimit-remaining-subscription-reads</span></span> |<span data-ttu-id="11b4b-121">Kalan abonelik kapsamlı okur</span><span class="sxs-lookup"><span data-stu-id="11b4b-121">Subscription scoped reads remaining</span></span> |
| <span data-ttu-id="11b4b-122">x-MS-ratelimit-Remaining-Subscription-Writes</span><span class="sxs-lookup"><span data-stu-id="11b4b-122">x-ms-ratelimit-remaining-subscription-writes</span></span> |<span data-ttu-id="11b4b-123">Kalan abonelik kapsamlı Yazar</span><span class="sxs-lookup"><span data-stu-id="11b4b-123">Subscription scoped writes remaining</span></span> |
| <span data-ttu-id="11b4b-124">x-MS-ratelimit-Remaining-tenant-Reads</span><span class="sxs-lookup"><span data-stu-id="11b4b-124">x-ms-ratelimit-remaining-tenant-reads</span></span> |<span data-ttu-id="11b4b-125">Kalan kapsamlı kiracı okur</span><span class="sxs-lookup"><span data-stu-id="11b4b-125">Tenant scoped reads remaining</span></span> |
| <span data-ttu-id="11b4b-126">x-MS-ratelimit-Remaining-tenant-Writes</span><span class="sxs-lookup"><span data-stu-id="11b4b-126">x-ms-ratelimit-remaining-tenant-writes</span></span> |<span data-ttu-id="11b4b-127">Kalan kapsamlı Kiracı Yazar</span><span class="sxs-lookup"><span data-stu-id="11b4b-127">Tenant scoped writes remaining</span></span> |
| <span data-ttu-id="11b4b-128">x-MS-ratelimit-Remaining-Subscription-Resource-Requests</span><span class="sxs-lookup"><span data-stu-id="11b4b-128">x-ms-ratelimit-remaining-subscription-resource-requests</span></span> |<span data-ttu-id="11b4b-129">Abonelik, kaynak türü istekleri kalan kapsamlı.</span><span class="sxs-lookup"><span data-stu-id="11b4b-129">Subscription scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="11b4b-130">Bu üstbilgi değerini yalnızca bir hizmet varsayılan sınır kılınmış döndürülür.</span><span class="sxs-lookup"><span data-stu-id="11b4b-130">This header value is only returned if a service has overridden the default limit.</span></span> <span data-ttu-id="11b4b-131">Resource Manager abonelik okuma veya yazmaları yerine bu değer ekler.</span><span class="sxs-lookup"><span data-stu-id="11b4b-131">Resource Manager adds this value instead of the subscription reads or writes.</span></span> |
| <span data-ttu-id="11b4b-132">x-MS-ratelimit-Remaining-Subscription-Resource-entities-Read</span><span class="sxs-lookup"><span data-stu-id="11b4b-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span></span> |<span data-ttu-id="11b4b-133">Abonelik, kaynak türü koleksiyonu isteklerini kalan kapsamlı.</span><span class="sxs-lookup"><span data-stu-id="11b4b-133">Subscription scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="11b4b-134">Bu üstbilgi değerini yalnızca bir hizmet varsayılan sınır kılınmış döndürülür.</span><span class="sxs-lookup"><span data-stu-id="11b4b-134">This header value is only returned if a service has overridden the default limit.</span></span> <span data-ttu-id="11b4b-135">Bu değer kalan koleksiyonu isteklerini (liste kaynakları) sayısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="11b4b-135">This value provides the number of remaining collection requests (list resources).</span></span> |
| <span data-ttu-id="11b4b-136">x-MS-ratelimit-Remaining-tenant-Resource-Requests</span><span class="sxs-lookup"><span data-stu-id="11b4b-136">x-ms-ratelimit-remaining-tenant-resource-requests</span></span> |<span data-ttu-id="11b4b-137">Kiracı kaynak türü istekleri kalan kapsamlı.</span><span class="sxs-lookup"><span data-stu-id="11b4b-137">Tenant scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="11b4b-138">Bu üst yalnızca Kiracı düzeyinde istekleri için eklenir ve yalnızca bir hizmet varsayılan sınır geçersiz kılınmış.</span><span class="sxs-lookup"><span data-stu-id="11b4b-138">This header is only added for requests at tenant level, and only if a service has overridden the default limit.</span></span> <span data-ttu-id="11b4b-139">Resource Manager Kiracı okuma veya yazmaları yerine bu değer ekler.</span><span class="sxs-lookup"><span data-stu-id="11b4b-139">Resource Manager adds this value instead of the tenant reads or writes.</span></span> |
| <span data-ttu-id="11b4b-140">x-MS-ratelimit-Remaining-tenant-Resource-entities-Read</span><span class="sxs-lookup"><span data-stu-id="11b4b-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span></span> |<span data-ttu-id="11b4b-141">Kiracı kaynak türü koleksiyonu isteklerini kalan kapsamlı.</span><span class="sxs-lookup"><span data-stu-id="11b4b-141">Tenant scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="11b4b-142">Bu üst yalnızca Kiracı düzeyinde istekleri için eklenir ve yalnızca bir hizmet varsayılan sınır geçersiz kılınmış.</span><span class="sxs-lookup"><span data-stu-id="11b4b-142">This header is only added for requests at tenant level, and only if a service has overridden the default limit.</span></span> |

## <a name="retrieving-the-header-values"></a><span data-ttu-id="11b4b-143">Üstbilgi değerlerini alma</span><span class="sxs-lookup"><span data-stu-id="11b4b-143">Retrieving the header values</span></span>
<span data-ttu-id="11b4b-144">Kod ya da komut dosyasında bu üstbilgi değerlerini alma herhangi bir üstbilgi değeri almaktan farklı değildir.</span><span class="sxs-lookup"><span data-stu-id="11b4b-144">Retrieving these header values in your code or script is no different than retrieving any header value.</span></span> 

<span data-ttu-id="11b4b-145">Örneğin, **C#**, üstbilgi değeri almak bir **HttpWebResponse** adlı nesne **yanıt** aşağıdaki kod ile:</span><span class="sxs-lookup"><span data-stu-id="11b4b-145">For example, in **C#**, you retrieve the header value from an **HttpWebResponse** object named **response** with the following code:</span></span>

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

<span data-ttu-id="11b4b-146">İçinde **PowerShell**, bir Invoke-WebRequest işlemden üstbilgi değeri alır.</span><span class="sxs-lookup"><span data-stu-id="11b4b-146">In **PowerShell**, you retrieve the header value from an Invoke-WebRequest operation.</span></span>

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

<span data-ttu-id="11b4b-147">Veya, size sağlayabilir hata ayıklama, kalan isteklerini görmek istiyorsanız **-Debug** parametresi, **PowerShell** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="11b4b-147">Or, if want to see the remaining requests for debugging, you can provide the **-Debug** parameter on your **PowerShell** cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -Debug
```

<span data-ttu-id="11b4b-148">Aşağıdaki yanıt değeri de dahil olmak üzere birden fazla değer döndüren:</span><span class="sxs-lookup"><span data-stu-id="11b4b-148">Which returns many values, including the following response value:</span></span>

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

<span data-ttu-id="11b4b-149">İçinde **Azure CLI**, daha ayrıntılı seçeneğini kullanarak üstbilgi değerini alır.</span><span class="sxs-lookup"><span data-stu-id="11b4b-149">In **Azure CLI**, you retrieve the header value by using the more verbose option.</span></span>

```azurecli
azure group list -vv --json
```

<span data-ttu-id="11b4b-150">Aşağıdaki nesne dahil olmak üzere birden fazla değer döndüren:</span><span class="sxs-lookup"><span data-stu-id="11b4b-150">Which returns many values, including the following object:</span></span>

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

## <a name="waiting-before-sending-next-request"></a><span data-ttu-id="11b4b-151">Sonraki istek gönderilmeden önce bekleniyor</span><span class="sxs-lookup"><span data-stu-id="11b4b-151">Waiting before sending next request</span></span>
<span data-ttu-id="11b4b-152">İstek sınırına ulaştığında, Resource Manager döndürür **429** HTTP durum kodu ve **yeniden deneme sonrasında** üstbilgi değeri.</span><span class="sxs-lookup"><span data-stu-id="11b4b-152">When you reach the request limit, Resource Manager returns the **429** HTTP status code and a **Retry-After** value in the header.</span></span> <span data-ttu-id="11b4b-153">**Yeniden deneme sonrasında** değeri sonraki istek göndermeden önce uygulamanızın beklemesi gereken saniye (veya uyku) sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="11b4b-153">The **Retry-After** value specifies the number of seconds your application should wait (or sleep) before sending the next request.</span></span> <span data-ttu-id="11b4b-154">Yeniden deneme değeri geçmeden önce bir isteği gönderirseniz, isteğiniz işlenmedi ve yeni bir yeniden deneme değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="11b4b-154">If you send a request before the retry value has elapsed, your request is not processed and a new retry value is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11b4b-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="11b4b-155">Next steps</span></span>

* <span data-ttu-id="11b4b-156">Sınırları ve kotalar hakkında daha fazla bilgi için bkz: [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="11b4b-156">For more information about limits and quotas, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>
* <span data-ttu-id="11b4b-157">Zaman uyumsuz REST istekleri işleme hakkında bilgi edinmek için [izlemek zaman uyumsuz Azure işlemleri](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="11b4b-157">To learn about handling asynchronous REST requests, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
