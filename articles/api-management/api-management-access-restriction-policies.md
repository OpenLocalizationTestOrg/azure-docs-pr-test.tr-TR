---
title: "aaaAzure API Management erişimi kısıtlama ilkeleri | Microsoft Docs"
description: "Merhaba erişim kısıtlama ilkeleri kullanılmak üzere Azure API Management hakkında bilgi edinin."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 034febe3-465f-4840-9fc6-c448ef520b0f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 0ef368c2781d9a5cf9eaaa41a47489c904ed3198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-access-restriction-policies"></a><span data-ttu-id="be029-103">API yönetim erişim kısıtlama ilkeleri</span><span class="sxs-lookup"><span data-stu-id="be029-103">API Management access restriction policies</span></span>
<span data-ttu-id="be029-104">Bu konuda API Management ilkelere hello için bir başvuru sağlar.</span><span class="sxs-lookup"><span data-stu-id="be029-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="be029-105">Ekleme ve ilkeleri yapılandırma hakkında daha fazla bilgi için bkz: [API Management ilkeleri](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="be029-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="be029-106"><a name="AccessRestrictionPolicies"></a>Erişimi kısıtlama ilkeleri</span><span class="sxs-lookup"><span data-stu-id="be029-106"><a name="AccessRestrictionPolicies"></a> Access restriction policies</span></span>  
  
-   <span data-ttu-id="be029-107">[Onay HTTP üstbilgisi](api-management-access-restriction-policies.md#CheckHTTPHeader) -varlığı ve/veya bir HTTP üstbilgisi değerini zorlar.</span><span class="sxs-lookup"><span data-stu-id="be029-107">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
-   <span data-ttu-id="be029-108">[Abonelik tarafından çağrı hızını sınırla](api-management-access-restriction-policies.md#LimitCallRate) -engeller API kullanımı ani başına abonelik başına çağrı hızını sınırlayarak.</span><span class="sxs-lookup"><span data-stu-id="be029-108">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="be029-109">[Anahtara göre çağrı hızını sınırla](#LimitCallRateByKey) -engeller API kullanımı ani başına anahtar başına çağrı hızını sınırlayarak.</span><span class="sxs-lookup"><span data-stu-id="be029-109">[Limit call rate by key](#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
-   <span data-ttu-id="be029-110">[Arayan IP'leri kısıtlamak](api-management-access-restriction-policies.md#RestrictCallerIPs) -filtreleri (verir/engellediği) çağrılarından belirli IP adreslerini ve/veya adres aralığı.</span><span class="sxs-lookup"><span data-stu-id="be029-110">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
-   <span data-ttu-id="be029-111">[Abonelik tarafından kullanım kotası ayarla](api-management-access-restriction-policies.md#SetUsageQuota) -bir abonelik başına temelinde tooenforce yenilenebilir veya ömrü çağrısı birim ve/veya bant genişliği kotaya izin verir.</span><span class="sxs-lookup"><span data-stu-id="be029-111">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="be029-112">[Anahtara göre kullanım kotası ayarla](#SetUsageQuotaByKey) -bir anahtar başına temelinde tooenforce yenilenebilir veya ömrü çağrısı birim ve/veya bant genişliği kotaya izin verir.</span><span class="sxs-lookup"><span data-stu-id="be029-112">[Set usage quota by key](#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
-   <span data-ttu-id="be029-113">[JWT doğrulama](api-management-access-restriction-policies.md#ValidateJWT) -varlığı ve belirtilen bir HTTP üstbilgisi veya belirtilen sorgu parametresi ayıklanan JWT geçerliliğini zorlar.</span><span class="sxs-lookup"><span data-stu-id="be029-113">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
##  <span data-ttu-id="be029-114"><a name="CheckHTTPHeader"></a>HTTP üstbilgisi denetleyin</span><span class="sxs-lookup"><span data-stu-id="be029-114"><a name="CheckHTTPHeader"></a> Check HTTP header</span></span>  
 <span data-ttu-id="be029-115">Kullanım hello `check-header` İlkesi tooenforce bir istek belirtilen bir HTTP üstbilgisi vardır.</span><span class="sxs-lookup"><span data-stu-id="be029-115">Use hello `check-header` policy tooenforce that a request has a specified HTTP header.</span></span> <span data-ttu-id="be029-116">Belirli bir değer veya izin verilen değer aralığı için onay Hello üstbilgi varsa, isteğe bağlı olarak toosee kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be029-116">You can optionally check toosee if hello header has a specific value or check for a range of allowed values.</span></span> <span data-ttu-id="be029-117">Merhaba denetimi başarısız olursa hello İlkesi isteği işleme sonlandırır ve hello İlkesi tarafından belirtilen hello HTTP durum kodu ve hata iletisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="be029-117">If hello check fails, hello policy terminates request processing and returns hello HTTP status code and error message specified by hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="be029-118">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="be029-118">Policy statement</span></span>  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a><span data-ttu-id="be029-119">Örnek</span><span class="sxs-lookup"><span data-stu-id="be029-119">Example</span></span>  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a><span data-ttu-id="be029-120">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="be029-120">Elements</span></span>  
  
|<span data-ttu-id="be029-121">Ad</span><span class="sxs-lookup"><span data-stu-id="be029-121">Name</span></span>|<span data-ttu-id="be029-122">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be029-122">Description</span></span>|<span data-ttu-id="be029-123">Gerekli</span><span class="sxs-lookup"><span data-stu-id="be029-123">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="be029-124">onay üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="be029-124">check-header</span></span>|<span data-ttu-id="be029-125">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="be029-125">Root element.</span></span>|<span data-ttu-id="be029-126">Evet</span><span class="sxs-lookup"><span data-stu-id="be029-126">Yes</span></span>|  
|<span data-ttu-id="be029-127">değer</span><span class="sxs-lookup"><span data-stu-id="be029-127">value</span></span>|<span data-ttu-id="be029-128">İzin verilen HTTP üstbilgisi değeri.</span><span class="sxs-lookup"><span data-stu-id="be029-128">Allowed HTTP header value.</span></span> <span data-ttu-id="be029-129">Birden çok değer öğesi belirtildiğinde, herhangi bir hello değerlerin bir eşleşme varsa hello onay başarı olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="be029-129">When multiple value elements are specified, hello check is considered a success if any one of hello values is a match.</span></span>|<span data-ttu-id="be029-130">Hayır</span><span class="sxs-lookup"><span data-stu-id="be029-130">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="be029-131">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="be029-131">Attributes</span></span>  
  
|<span data-ttu-id="be029-132">Ad</span><span class="sxs-lookup"><span data-stu-id="be029-132">Name</span></span>|<span data-ttu-id="be029-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be029-133">Description</span></span>|<span data-ttu-id="be029-134">Gerekli</span><span class="sxs-lookup"><span data-stu-id="be029-134">Required</span></span>|<span data-ttu-id="be029-135">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="be029-135">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="be029-136">başarısız oldu-onay-hata iletisi</span><span class="sxs-lookup"><span data-stu-id="be029-136">failed-check-error-message</span></span>|<span data-ttu-id="be029-137">Hata iletisi tooreturn hello üstbilgi yok veya geçersiz bir değere sahip olursa hello HTTP yanıt gövdesi içinde.</span><span class="sxs-lookup"><span data-stu-id="be029-137">Error message tooreturn in hello HTTP response body if hello header doesn't exist or has an invalid value.</span></span> <span data-ttu-id="be029-138">Bu ileti, tüm özel karakterleri düzgün şekilde çıkıldığından olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="be029-138">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="be029-139">Evet</span><span class="sxs-lookup"><span data-stu-id="be029-139">Yes</span></span>|<span data-ttu-id="be029-140">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-140">N/A</span></span>|  
|<span data-ttu-id="be029-141">başarısız oldu-onay-httpcode</span><span class="sxs-lookup"><span data-stu-id="be029-141">failed-check-httpcode</span></span>|<span data-ttu-id="be029-142">HTTP durum kodu tooreturn Hello üstbilgi yok veya geçersiz bir değere sahip.</span><span class="sxs-lookup"><span data-stu-id="be029-142">HTTP Status code tooreturn if hello header doesn't exist or has an invalid value.</span></span>|<span data-ttu-id="be029-143">Evet</span><span class="sxs-lookup"><span data-stu-id="be029-143">Yes</span></span>|<span data-ttu-id="be029-144">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-144">N/A</span></span>|  
|<span data-ttu-id="be029-145">üstbilgi adı</span><span class="sxs-lookup"><span data-stu-id="be029-145">header-name</span></span>|<span data-ttu-id="be029-146">Merhaba HTTP üstbilgisi toocheck Hello adı.</span><span class="sxs-lookup"><span data-stu-id="be029-146">hello name of hello HTTP Header toocheck.</span></span>|<span data-ttu-id="be029-147">Evet</span><span class="sxs-lookup"><span data-stu-id="be029-147">Yes</span></span>|<span data-ttu-id="be029-148">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-148">N/A</span></span>|  
|<span data-ttu-id="be029-149">Yoksay durumu</span><span class="sxs-lookup"><span data-stu-id="be029-149">ignore-case</span></span>|<span data-ttu-id="be029-150">TooTrue ya da yanlış ayarlanmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="be029-150">Can be set tooTrue or False.</span></span> <span data-ttu-id="be029-151">Merhaba üstbilgi değeri kabul edilebilir değerler hello kümesi karşı karşılaştırıldığında kümesi tooTrue durum göz ardı gerekiyorsa.</span><span class="sxs-lookup"><span data-stu-id="be029-151">If set tooTrue case is ignored when hello header value is compared against hello set of acceptable values.</span></span>|<span data-ttu-id="be029-152">Evet</span><span class="sxs-lookup"><span data-stu-id="be029-152">Yes</span></span>|<span data-ttu-id="be029-153">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-153">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="be029-154">Kullanım</span><span class="sxs-lookup"><span data-stu-id="be029-154">Usage</span></span>  
 <span data-ttu-id="be029-155">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="be029-155">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="be029-156">**İlke bölümleri:** gelen, giden</span><span class="sxs-lookup"><span data-stu-id="be029-156">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="be029-157">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="be029-157">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="be029-158"><a name="LimitCallRate"></a>Abonelik tarafından çağrı hızını sınırla</span><span class="sxs-lookup"><span data-stu-id="be029-158"><a name="LimitCallRate"></a> Limit call rate by subscription</span></span>  
 <span data-ttu-id="be029-159">Merhaba `rate-limit` ilke engeller API kullanımı ani hello sınırlayarak abonelik başına temelinde oranı tooa belirtilen belirli bir süre sayı çağırın.</span><span class="sxs-lookup"><span data-stu-id="be029-159">hello `rate-limit` policy prevents API usage spikes on a per subscription basis by limiting hello call rate tooa specified number per a specified time period.</span></span> <span data-ttu-id="be029-160">Bu ilke tetiklendiğinde hello arayan alan bir `429 Too Many Requests` yanıt durum kodu.</span><span class="sxs-lookup"><span data-stu-id="be029-160">When this policy is triggered hello caller receives a `429 Too Many Requests` response status code.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="be029-161">Bu ilke, ilke belge başına yalnızca bir kez kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="be029-161">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="be029-162">[İlke ifadeleri](api-management-policy-expressions.md) hello İlkesi özniteliklerini hiçbirinde Bu ilke için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="be029-162">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="be029-163">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="be029-163">Policy statement</span></span>  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a><span data-ttu-id="be029-164">Örnek</span><span class="sxs-lookup"><span data-stu-id="be029-164">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit calls="20" renewal-period="90" />  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="be029-165">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="be029-165">Elements</span></span>  
  
|<span data-ttu-id="be029-166">Ad</span><span class="sxs-lookup"><span data-stu-id="be029-166">Name</span></span>|<span data-ttu-id="be029-167">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be029-167">Description</span></span>|<span data-ttu-id="be029-168">Gerekli</span><span class="sxs-lookup"><span data-stu-id="be029-168">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="be029-169">sınırını ayarlama</span><span class="sxs-lookup"><span data-stu-id="be029-169">set-limit</span></span>|<span data-ttu-id="be029-170">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="be029-170">Root element.</span></span>|<span data-ttu-id="be029-171">Evet</span><span class="sxs-lookup"><span data-stu-id="be029-171">Yes</span></span>|  
|<span data-ttu-id="be029-172">api</span><span class="sxs-lookup"><span data-stu-id="be029-172">api</span></span>|<span data-ttu-id="be029-173">Bir veya daha fazla bu öğeleri tooimpose çağrı hızı sınırı API'leri hello ürün içinde ekleyin.</span><span class="sxs-lookup"><span data-stu-id="be029-173">Add one  or more of these elements tooimpose a call rate limit on APIs within hello product.</span></span> <span data-ttu-id="be029-174">Ürün ve API sınırları bağımsız olarak uygulanır oranı arayın.</span><span class="sxs-lookup"><span data-stu-id="be029-174">Product and API call rate limits are applied independently.</span></span>|<span data-ttu-id="be029-175">Hayır</span><span class="sxs-lookup"><span data-stu-id="be029-175">No</span></span>|  
|<span data-ttu-id="be029-176">işlemi</span><span class="sxs-lookup"><span data-stu-id="be029-176">operation</span></span>|<span data-ttu-id="be029-177">Bir veya daha fazla bu öğeleri tooimpose çağrı hızı sınırı bir API işlemlerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="be029-177">Add one  or more of these elements tooimpose a call rate limit on operations within an API.</span></span> <span data-ttu-id="be029-178">Ürün, API ve işlem sınırları bağımsız olarak uygulanır oranı çağırın.</span><span class="sxs-lookup"><span data-stu-id="be029-178">Product, API, and operation call rate limits are applied independently.</span></span>|<span data-ttu-id="be029-179">Hayır</span><span class="sxs-lookup"><span data-stu-id="be029-179">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="be029-180">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="be029-180">Attributes</span></span>  
  
|<span data-ttu-id="be029-181">Ad</span><span class="sxs-lookup"><span data-stu-id="be029-181">Name</span></span>|<span data-ttu-id="be029-182">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be029-182">Description</span></span>|<span data-ttu-id="be029-183">Gerekli</span><span class="sxs-lookup"><span data-stu-id="be029-183">Required</span></span>|<span data-ttu-id="be029-184">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="be029-184">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="be029-185">ad</span><span class="sxs-lookup"><span data-stu-id="be029-185">name</span></span>|<span data-ttu-id="be029-186">hangi tooapply hello hızı sınırı hello API adı Hello.</span><span class="sxs-lookup"><span data-stu-id="be029-186">hello name of hello API for which tooapply hello rate limit.</span></span>|<span data-ttu-id="be029-187">Evet</span><span class="sxs-lookup"><span data-stu-id="be029-187">Yes</span></span>|<span data-ttu-id="be029-188">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-188">N/A</span></span>|  
|<span data-ttu-id="be029-189">çağrıları</span><span class="sxs-lookup"><span data-stu-id="be029-189">calls</span></span>|<span data-ttu-id="be029-190">Merhaba çağrıları hello belirtilen hello zaman aralığı boyunca izin verilen en fazla toplam sayısı `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="be029-190">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="be029-191">Evet</span><span class="sxs-lookup"><span data-stu-id="be029-191">Yes</span></span>|<span data-ttu-id="be029-192">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-192">N/A</span></span>|  
|<span data-ttu-id="be029-193">yenileme dönemi</span><span class="sxs-lookup"><span data-stu-id="be029-193">renewal-period</span></span>|<span data-ttu-id="be029-194">Merhaba zaman aralığını saniye olarak geçmesi hello kota sıfırlar.</span><span class="sxs-lookup"><span data-stu-id="be029-194">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="be029-195">Evet</span><span class="sxs-lookup"><span data-stu-id="be029-195">Yes</span></span>|<span data-ttu-id="be029-196">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-196">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="be029-197">Kullanım</span><span class="sxs-lookup"><span data-stu-id="be029-197">Usage</span></span>  
 <span data-ttu-id="be029-198">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="be029-198">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="be029-199">**İlke bölümleri:** gelen</span><span class="sxs-lookup"><span data-stu-id="be029-199">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="be029-200">**İlke kapsamları:** ürün</span><span class="sxs-lookup"><span data-stu-id="be029-200">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="be029-201"><a name="LimitCallRateByKey"></a>Anahtara göre çağrı hızını sınırla</span><span class="sxs-lookup"><span data-stu-id="be029-201"><a name="LimitCallRateByKey"></a> Limit call rate by key</span></span>  
 <span data-ttu-id="be029-202">Merhaba `rate-limit-by-key` ilke engeller API kullanımı ani hello sınırlayarak anahtar başına temelinde oranı tooa belirtilen belirli bir süre sayı çağırın.</span><span class="sxs-lookup"><span data-stu-id="be029-202">hello `rate-limit-by-key` policy prevents API usage spikes on a per key basis by limiting hello call rate tooa specified number per a specified time period.</span></span> <span data-ttu-id="be029-203">Merhaba anahtar bir isteğe bağlı bir dize değerine sahip olabilir ve genellikle bir ilke ifade kullanılarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="be029-203">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="be029-204">İsteğe bağlı increment koşulu, hangi isteklerinin hello sınırında sayılması toospecify eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="be029-204">Optional increment condition can be added toospecify which requests should be counted towards hello limit.</span></span> <span data-ttu-id="be029-205">Bu ilke tetiklendiğinde hello arayan alan bir `429 Too Many Requests` yanıt durum kodu.</span><span class="sxs-lookup"><span data-stu-id="be029-205">When this policy is triggered hello caller receives a `429 Too Many Requests` response status code.</span></span>  
  
 <span data-ttu-id="be029-206">Daha fazla bilgi ve bu ilkeyi örnekleri için bkz: [Gelişmiş istek azaltma Azure API Management ile](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="be029-206">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="be029-207">Bu ilke, ilke belge başına yalnızca bir kez kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="be029-207">This policy can be used only once per policy document.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="be029-208">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="be029-208">Policy statement</span></span>  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="be029-209">Örnek</span><span class="sxs-lookup"><span data-stu-id="be029-209">Example</span></span>  
 <span data-ttu-id="be029-210">Aşağıdaki örneğine hello hello hızı sınırı hello arayan IP adresine göre anahtarlanır.</span><span class="sxs-lookup"><span data-stu-id="be029-210">In hello following example, hello rate limit is keyed by hello caller IP address.</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit-by-key  calls="10"  
              renewal-period="60"  
              increment-condition="@(context.Response.StatusCode == 200)"  
              counter-key="@(context.Request.IpAddress)"/>  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="be029-211">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="be029-211">Elements</span></span>  
  
|<span data-ttu-id="be029-212">Ad</span><span class="sxs-lookup"><span data-stu-id="be029-212">Name</span></span>|<span data-ttu-id="be029-213">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be029-213">Description</span></span>|<span data-ttu-id="be029-214">Gerekli</span><span class="sxs-lookup"><span data-stu-id="be029-214">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="be029-215">sınırını ayarlama</span><span class="sxs-lookup"><span data-stu-id="be029-215">set-limit</span></span>|<span data-ttu-id="be029-216">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="be029-216">Root element.</span></span>|<span data-ttu-id="be029-217">Evet</span><span class="sxs-lookup"><span data-stu-id="be029-217">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="be029-218">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="be029-218">Attributes</span></span>  
  
|<span data-ttu-id="be029-219">Ad</span><span class="sxs-lookup"><span data-stu-id="be029-219">Name</span></span>|<span data-ttu-id="be029-220">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be029-220">Description</span></span>|<span data-ttu-id="be029-221">Gerekli</span><span class="sxs-lookup"><span data-stu-id="be029-221">Required</span></span>|<span data-ttu-id="be029-222">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="be029-222">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="be029-223">çağrıları</span><span class="sxs-lookup"><span data-stu-id="be029-223">calls</span></span>|<span data-ttu-id="be029-224">Merhaba çağrıları hello belirtilen hello zaman aralığı boyunca izin verilen en fazla toplam sayısı `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="be029-224">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="be029-225">Evet</span><span class="sxs-lookup"><span data-stu-id="be029-225">Yes</span></span>|<span data-ttu-id="be029-226">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-226">N/A</span></span>|  
|<span data-ttu-id="be029-227">Tamamlayıcı anahtarı</span><span class="sxs-lookup"><span data-stu-id="be029-227">counter-key</span></span>|<span data-ttu-id="be029-228">Merhaba hello hız sınırı ilkesi için anahtar toouse.</span><span class="sxs-lookup"><span data-stu-id="be029-228">hello key toouse for hello rate limit policy.</span></span>|<span data-ttu-id="be029-229">Evet</span><span class="sxs-lookup"><span data-stu-id="be029-229">Yes</span></span>|<span data-ttu-id="be029-230">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-230">N/A</span></span>|  
|<span data-ttu-id="be029-231">Koşul artırma</span><span class="sxs-lookup"><span data-stu-id="be029-231">increment-condition</span></span>|<span data-ttu-id="be029-232">Merhaba isteği hello kota sayılan olmadığını belirten hello Boole ifadesi (`true`).</span><span class="sxs-lookup"><span data-stu-id="be029-232">hello boolean expression specifying if hello request should be counted towards hello quota (`true`).</span></span>|<span data-ttu-id="be029-233">Hayır</span><span class="sxs-lookup"><span data-stu-id="be029-233">No</span></span>|<span data-ttu-id="be029-234">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-234">N/A</span></span>|  
|<span data-ttu-id="be029-235">yenileme dönemi</span><span class="sxs-lookup"><span data-stu-id="be029-235">renewal-period</span></span>|<span data-ttu-id="be029-236">Merhaba zaman aralığını saniye olarak geçmesi hello kota sıfırlar.</span><span class="sxs-lookup"><span data-stu-id="be029-236">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="be029-237">Evet</span><span class="sxs-lookup"><span data-stu-id="be029-237">Yes</span></span>|<span data-ttu-id="be029-238">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-238">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="be029-239">Kullanım</span><span class="sxs-lookup"><span data-stu-id="be029-239">Usage</span></span>  
 <span data-ttu-id="be029-240">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="be029-240">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="be029-241">**İlke bölümleri:** gelen</span><span class="sxs-lookup"><span data-stu-id="be029-241">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="be029-242">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="be029-242">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="be029-243"><a name="RestrictCallerIPs"></a>Arayan IP'leri kısıtla</span><span class="sxs-lookup"><span data-stu-id="be029-243"><a name="RestrictCallerIPs"></a> Restrict caller IPs</span></span>  
 <span data-ttu-id="be029-244">Merhaba `ip-filter` ilke filtrelerini belirli IP adreslerini ve/veya adres aralıklarını gelen çağrıları (verir/engeller).</span><span class="sxs-lookup"><span data-stu-id="be029-244">hello `ip-filter` policy filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="be029-245">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="be029-245">Policy statement</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a><span data-ttu-id="be029-246">Örnek</span><span class="sxs-lookup"><span data-stu-id="be029-246">Example</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a><span data-ttu-id="be029-247">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="be029-247">Elements</span></span>  
  
|<span data-ttu-id="be029-248">Ad</span><span class="sxs-lookup"><span data-stu-id="be029-248">Name</span></span>|<span data-ttu-id="be029-249">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be029-249">Description</span></span>|<span data-ttu-id="be029-250">Gerekli</span><span class="sxs-lookup"><span data-stu-id="be029-250">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="be029-251">IP Filtresi</span><span class="sxs-lookup"><span data-stu-id="be029-251">ip-filter</span></span>|<span data-ttu-id="be029-252">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="be029-252">Root element.</span></span>|<span data-ttu-id="be029-253">Evet</span><span class="sxs-lookup"><span data-stu-id="be029-253">Yes</span></span>|  
|<span data-ttu-id="be029-254">Adres</span><span class="sxs-lookup"><span data-stu-id="be029-254">address</span></span>|<span data-ttu-id="be029-255">Tek bir IP adresi üzerinde hangi toofilter belirtir.</span><span class="sxs-lookup"><span data-stu-id="be029-255">Specifies a single IP address on which toofilter.</span></span>|<span data-ttu-id="be029-256">En az bir `address` veya `address-range` öğesi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="be029-256">At least one `address` or `address-range` element is required.</span></span>|  
|<span data-ttu-id="be029-257">adres aralığı adresinden ="" için "Adres" =</span><span class="sxs-lookup"><span data-stu-id="be029-257">address-range from="address" to="address"</span></span>|<span data-ttu-id="be029-258">Bir IP adresi aralığı üzerinde hangi toofilter belirtir.</span><span class="sxs-lookup"><span data-stu-id="be029-258">Specifies a range of IP address on which toofilter.</span></span>|<span data-ttu-id="be029-259">En az bir `address` veya `address-range` öğesi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="be029-259">At least one `address` or `address-range` element is required.</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="be029-260">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="be029-260">Attributes</span></span>  
  
|<span data-ttu-id="be029-261">Ad</span><span class="sxs-lookup"><span data-stu-id="be029-261">Name</span></span>|<span data-ttu-id="be029-262">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be029-262">Description</span></span>|<span data-ttu-id="be029-263">Gerekli</span><span class="sxs-lookup"><span data-stu-id="be029-263">Required</span></span>|<span data-ttu-id="be029-264">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="be029-264">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="be029-265">adres aralığı adresinden ="" için "Adres" =</span><span class="sxs-lookup"><span data-stu-id="be029-265">address-range from="address" to="address"</span></span>|<span data-ttu-id="be029-266">Bir dizi IP tooallow adresleri veya erişimi reddetmek.</span><span class="sxs-lookup"><span data-stu-id="be029-266">A range of IP addresses tooallow or deny access for.</span></span>|<span data-ttu-id="be029-267">Merhaba gereklidir `address-range` öğe kullanılır.</span><span class="sxs-lookup"><span data-stu-id="be029-267">Required when hello `address-range` element is used.</span></span>|<span data-ttu-id="be029-268">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-268">N/A</span></span>|  
|<span data-ttu-id="be029-269">IP filtre eylemi = "izin &#124; yasaklamaz"</span><span class="sxs-lookup"><span data-stu-id="be029-269">ip-filter action="allow &#124; forbid"</span></span>|<span data-ttu-id="be029-270">Çağrıları izin verilmesi veya IP adresleri ve aralıkları değil hello için belirtilen olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="be029-270">Specifies whether calls should be allowed or not for hello specified IP addresses and ranges.</span></span>|<span data-ttu-id="be029-271">Evet</span><span class="sxs-lookup"><span data-stu-id="be029-271">Yes</span></span>|<span data-ttu-id="be029-272">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="be029-273">Kullanım</span><span class="sxs-lookup"><span data-stu-id="be029-273">Usage</span></span>  
 <span data-ttu-id="be029-274">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="be029-274">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="be029-275">**İlke bölümleri:** gelen</span><span class="sxs-lookup"><span data-stu-id="be029-275">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="be029-276">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="be029-276">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="be029-277"><a name="SetUsageQuota"></a>Abonelik tarafından kullanım kotası ayarla</span><span class="sxs-lookup"><span data-stu-id="be029-277"><a name="SetUsageQuota"></a> Set usage quota by subscription</span></span>  
 <span data-ttu-id="be029-278">Merhaba `quota` ilke yenilenebilir veya ömrü çağrısı birim ve/veya bant genişliği kota, abonelik başına temelinde zorunlu tutar.</span><span class="sxs-lookup"><span data-stu-id="be029-278">hello `quota` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="be029-279">Bu ilke, ilke belge başına yalnızca bir kez kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="be029-279">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="be029-280">[İlke ifadeleri](api-management-policy-expressions.md) hello İlkesi özniteliklerini hiçbirinde Bu ilke için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="be029-280">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="be029-281">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="be029-281">Policy statement</span></span>  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a><span data-ttu-id="be029-282">Örnek</span><span class="sxs-lookup"><span data-stu-id="be029-282">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota calls="10000" bandwidth="40000" renewal-period="3600" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="be029-283">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="be029-283">Elements</span></span>  
  
|<span data-ttu-id="be029-284">Ad</span><span class="sxs-lookup"><span data-stu-id="be029-284">Name</span></span>|<span data-ttu-id="be029-285">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be029-285">Description</span></span>|<span data-ttu-id="be029-286">Gerekli</span><span class="sxs-lookup"><span data-stu-id="be029-286">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="be029-287">Kota</span><span class="sxs-lookup"><span data-stu-id="be029-287">quota</span></span>|<span data-ttu-id="be029-288">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="be029-288">Root element.</span></span>|<span data-ttu-id="be029-289">Evet</span><span class="sxs-lookup"><span data-stu-id="be029-289">Yes</span></span>|  
|<span data-ttu-id="be029-290">api</span><span class="sxs-lookup"><span data-stu-id="be029-290">api</span></span>|<span data-ttu-id="be029-291">Bir veya daha fazla bu öğeleri tooimpose kota API'leri hello ürün içinde ekleyin.</span><span class="sxs-lookup"><span data-stu-id="be029-291">Add one  or more of these elements tooimpose a quota on APIs within hello product.</span></span> <span data-ttu-id="be029-292">Ürün ve API kotaları bağımsız olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="be029-292">Product and API quotas are applied independently.</span></span>|<span data-ttu-id="be029-293">Hayır</span><span class="sxs-lookup"><span data-stu-id="be029-293">No</span></span>|  
|<span data-ttu-id="be029-294">işlemi</span><span class="sxs-lookup"><span data-stu-id="be029-294">operation</span></span>|<span data-ttu-id="be029-295">Bir veya daha fazla bu öğeleri tooimpose kota bir API işlemlerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="be029-295">Add one  or more of these elements tooimpose a quota on operations within an API.</span></span> <span data-ttu-id="be029-296">Ürün, API ve işlem kotaları bağımsız olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="be029-296">Product, API, and operation quotas are applied independently.</span></span>|<span data-ttu-id="be029-297">Hayır</span><span class="sxs-lookup"><span data-stu-id="be029-297">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="be029-298">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="be029-298">Attributes</span></span>  
  
|<span data-ttu-id="be029-299">Ad</span><span class="sxs-lookup"><span data-stu-id="be029-299">Name</span></span>|<span data-ttu-id="be029-300">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be029-300">Description</span></span>|<span data-ttu-id="be029-301">Gerekli</span><span class="sxs-lookup"><span data-stu-id="be029-301">Required</span></span>|<span data-ttu-id="be029-302">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="be029-302">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="be029-303">ad</span><span class="sxs-lookup"><span data-stu-id="be029-303">name</span></span>|<span data-ttu-id="be029-304">Merhaba adı hello API veya işlemi için hangi hello kota uygulanır.</span><span class="sxs-lookup"><span data-stu-id="be029-304">hello name of hello API or operation for which hello quota applies.</span></span>|<span data-ttu-id="be029-305">Evet</span><span class="sxs-lookup"><span data-stu-id="be029-305">Yes</span></span>|<span data-ttu-id="be029-306">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-306">N/A</span></span>|  
|<span data-ttu-id="be029-307">Bant genişliği</span><span class="sxs-lookup"><span data-stu-id="be029-307">bandwidth</span></span>|<span data-ttu-id="be029-308">Merhaba kilobayt hello belirtilen hello zaman aralığı boyunca izin verilen en fazla toplam sayısı `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="be029-308">hello maximum total number of kilobytes allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="be029-309">Her iki `calls`, `bandwidth`, veya her ikisini de birlikte belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="be029-309">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="be029-310">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-310">N/A</span></span>|  
|<span data-ttu-id="be029-311">çağrıları</span><span class="sxs-lookup"><span data-stu-id="be029-311">calls</span></span>|<span data-ttu-id="be029-312">Merhaba çağrıları hello belirtilen hello zaman aralığı boyunca izin verilen en fazla toplam sayısı `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="be029-312">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="be029-313">Her iki `calls`, `bandwidth`, veya her ikisini de birlikte belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="be029-313">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="be029-314">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-314">N/A</span></span>|  
|<span data-ttu-id="be029-315">yenileme dönemi</span><span class="sxs-lookup"><span data-stu-id="be029-315">renewal-period</span></span>|<span data-ttu-id="be029-316">Merhaba zaman aralığını saniye olarak geçmesi hello kota sıfırlar.</span><span class="sxs-lookup"><span data-stu-id="be029-316">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="be029-317">Evet</span><span class="sxs-lookup"><span data-stu-id="be029-317">Yes</span></span>|<span data-ttu-id="be029-318">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-318">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="be029-319">Kullanım</span><span class="sxs-lookup"><span data-stu-id="be029-319">Usage</span></span>  
 <span data-ttu-id="be029-320">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="be029-320">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="be029-321">**İlke bölümleri:** gelen</span><span class="sxs-lookup"><span data-stu-id="be029-321">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="be029-322">**İlke kapsamları:** ürün</span><span class="sxs-lookup"><span data-stu-id="be029-322">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="be029-323"><a name="SetUsageQuotaByKey"></a>Anahtara göre kullanım kotası ayarla</span><span class="sxs-lookup"><span data-stu-id="be029-323"><a name="SetUsageQuotaByKey"></a> Set usage quota by key</span></span>  
 <span data-ttu-id="be029-324">Merhaba `quota-by-key` ilke yenilenebilir veya ömrü çağrısı birim ve/veya bant genişliği kota anahtarı başına temelinde zorunlu tutar.</span><span class="sxs-lookup"><span data-stu-id="be029-324">hello `quota-by-key` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span> <span data-ttu-id="be029-325">Merhaba anahtar bir isteğe bağlı bir dize değerine sahip olabilir ve genellikle bir ilke ifade kullanılarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="be029-325">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="be029-326">İsteğe bağlı increment koşulu, hangi istekler hello kota sayılması toospecify eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="be029-326">Optional increment condition can be added toospecify which requests should be counted towards hello quota.</span></span>  
  
 <span data-ttu-id="be029-327">Daha fazla bilgi ve bu ilkeyi örnekleri için bkz: [Gelişmiş istek azaltma Azure API Management ile](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="be029-327">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="be029-328">Bu ilke, ilke belge başına yalnızca bir kez kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="be029-328">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="be029-329">[İlke ifadeleri](api-management-policy-expressions.md) hello İlkesi özniteliklerini hiçbirinde Bu ilke için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="be029-329">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="be029-330">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="be029-330">Policy statement</span></span>  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="be029-331">Örnek</span><span class="sxs-lookup"><span data-stu-id="be029-331">Example</span></span>  
 <span data-ttu-id="be029-332">Aşağıdaki örneğine hello hello kota hello arayan IP adresine göre anahtarlanır.</span><span class="sxs-lookup"><span data-stu-id="be029-332">In hello following example, hello quota is keyed by hello caller IP address.</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota-by-key calls="10000" bandwidth="40000" renewal-period="3600"  
                      increment-condition="@(context.Response.StatusCode >= 200 && context.Response.StatusCode < 400)"  
                      counter-key="@(context.Request.IpAddress)" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="be029-333">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="be029-333">Elements</span></span>  
  
|<span data-ttu-id="be029-334">Ad</span><span class="sxs-lookup"><span data-stu-id="be029-334">Name</span></span>|<span data-ttu-id="be029-335">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be029-335">Description</span></span>|<span data-ttu-id="be029-336">Gerekli</span><span class="sxs-lookup"><span data-stu-id="be029-336">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="be029-337">Kota</span><span class="sxs-lookup"><span data-stu-id="be029-337">quota</span></span>|<span data-ttu-id="be029-338">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="be029-338">Root element.</span></span>|<span data-ttu-id="be029-339">Evet</span><span class="sxs-lookup"><span data-stu-id="be029-339">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="be029-340">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="be029-340">Attributes</span></span>  
  
|<span data-ttu-id="be029-341">Ad</span><span class="sxs-lookup"><span data-stu-id="be029-341">Name</span></span>|<span data-ttu-id="be029-342">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be029-342">Description</span></span>|<span data-ttu-id="be029-343">Gerekli</span><span class="sxs-lookup"><span data-stu-id="be029-343">Required</span></span>|<span data-ttu-id="be029-344">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="be029-344">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="be029-345">Bant genişliği</span><span class="sxs-lookup"><span data-stu-id="be029-345">bandwidth</span></span>|<span data-ttu-id="be029-346">Merhaba kilobayt hello belirtilen hello zaman aralığı boyunca izin verilen en fazla toplam sayısı `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="be029-346">hello maximum total number of kilobytes allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="be029-347">Her iki `calls`, `bandwidth`, veya her ikisini de birlikte belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="be029-347">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="be029-348">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-348">N/A</span></span>|  
|<span data-ttu-id="be029-349">çağrıları</span><span class="sxs-lookup"><span data-stu-id="be029-349">calls</span></span>|<span data-ttu-id="be029-350">Merhaba çağrıları hello belirtilen hello zaman aralığı boyunca izin verilen en fazla toplam sayısı `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="be029-350">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="be029-351">Her iki `calls`, `bandwidth`, veya her ikisini de birlikte belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="be029-351">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="be029-352">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-352">N/A</span></span>|  
|<span data-ttu-id="be029-353">Tamamlayıcı anahtarı</span><span class="sxs-lookup"><span data-stu-id="be029-353">counter-key</span></span>|<span data-ttu-id="be029-354">Merhaba hello kota ilkesi için anahtar toouse.</span><span class="sxs-lookup"><span data-stu-id="be029-354">hello key toouse for hello quota policy.</span></span>|<span data-ttu-id="be029-355">Evet</span><span class="sxs-lookup"><span data-stu-id="be029-355">Yes</span></span>|<span data-ttu-id="be029-356">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-356">N/A</span></span>|  
|<span data-ttu-id="be029-357">Koşul artırma</span><span class="sxs-lookup"><span data-stu-id="be029-357">increment-condition</span></span>|<span data-ttu-id="be029-358">Merhaba isteği hello kota sayılan olmadığını belirten hello Boole ifadesi (`true`)</span><span class="sxs-lookup"><span data-stu-id="be029-358">hello boolean expression specifying if hello request should be counted towards hello quota (`true`)</span></span>|<span data-ttu-id="be029-359">Hayır</span><span class="sxs-lookup"><span data-stu-id="be029-359">No</span></span>|<span data-ttu-id="be029-360">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-360">N/A</span></span>|  
|<span data-ttu-id="be029-361">yenileme dönemi</span><span class="sxs-lookup"><span data-stu-id="be029-361">renewal-period</span></span>|<span data-ttu-id="be029-362">Merhaba zaman aralığını saniye olarak geçmesi hello kota sıfırlar.</span><span class="sxs-lookup"><span data-stu-id="be029-362">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="be029-363">Evet</span><span class="sxs-lookup"><span data-stu-id="be029-363">Yes</span></span>|<span data-ttu-id="be029-364">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-364">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="be029-365">Kullanım</span><span class="sxs-lookup"><span data-stu-id="be029-365">Usage</span></span>  
 <span data-ttu-id="be029-366">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="be029-366">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="be029-367">**İlke bölümleri:** gelen</span><span class="sxs-lookup"><span data-stu-id="be029-367">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="be029-368">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="be029-368">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="be029-369"><a name="ValidateJWT"></a>JWT doğrula</span><span class="sxs-lookup"><span data-stu-id="be029-369"><a name="ValidateJWT"></a> Validate JWT</span></span>  
 <span data-ttu-id="be029-370">Merhaba `validate-jwt` İlkesi varlığı zorunlu kılan ve HTTP üstbilgisi veya belirtilen sorgu parametresi JWT geçerliliğini ya da belirtilen bir ayıklanır.</span><span class="sxs-lookup"><span data-stu-id="be029-370">hello `validate-jwt` policy enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="be029-371">Merhaba `validate-jwt` ilke gerektiriyorsa Bu hello `exp` kayıtlı talep olduğu hello JWT belirteci inlcuded sürece `require-expiration-time` öznitelik belirtilen ve çok ayarlayın`false`.</span><span class="sxs-lookup"><span data-stu-id="be029-371">hello `validate-jwt` policy requires that hello `exp` registered claim is inlcuded in hello JWT token, unless `require-expiration-time` attribute is specified and set too`false`.</span></span>  
> <span data-ttu-id="be029-372">Merhaba `validate-jwt` İlkesi HS256 ve RS256 imza algoritmaları destekler.</span><span class="sxs-lookup"><span data-stu-id="be029-372">hello `validate-jwt` policy supports HS256 and RS256 signing algorithms.</span></span> <span data-ttu-id="be029-373">HS256 için başlangıç anahtarı hello İlkesi'nde hello base64 ile kodlanmış form içi sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="be029-373">For HS256 hello key must be provided inline within hello policy in hello base64 encoded form.</span></span> <span data-ttu-id="be029-374">RS256 için bir Open ID yapılandırma uç noktası aracılığıyla sağlamak toobe hello anahtarı yok.</span><span class="sxs-lookup"><span data-stu-id="be029-374">For RS256 hello key has toobe provide via an Open ID configuration endpoint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="be029-375">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="be029-375">Policy statement</span></span>  
  
```xml  
<validate-jwt   
    header-name="name of http header containing hello token (use query-parameter-name attribute if hello token is passed in hello URL)"   
    failed-validation-httpcode="http status code tooreturn on failure"   
    failed-validation-error-message="error message tooreturn on failure"   
    require-expiration-time="true|false"
    require-scheme="scheme"
    require-signed-tokens="true|false"   
    clock-skew="allowed clock skew in seconds">  
  <issuer-signing-keys>  
    <key>base64 encoded signing key</key>  
    <!-- if there are multiple keys, then add additional key elements -->  
  </issuer-signing-keys>  
  <audiences>  
    <audience>audience string</audience>  
    <!-- if there are multiple possible audiences, then add additional audience elements -->  
  </audiences>  
  <issuers>  
    <issuer>issuer string</issuer>  
    <!-- if there are multiple possible issuers, then add additional issuer elements -->  
  </issuers>  
  <required-claims>  
    <claim name="name of hello claim as it appears in hello token" match="all|any">  
      <value>claim value as it is expected tooappear in hello token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of hello configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="be029-376">Örnekler</span><span class="sxs-lookup"><span data-stu-id="be029-376">Examples</span></span>  
  
#### <a name="azure-mobile-services-token-validation"></a><span data-ttu-id="be029-377">Azure Mobile Services belirteci doğrulama</span><span class="sxs-lookup"><span data-stu-id="be029-377">Azure Mobile Services token validation</span></span>  
  
```xml  
<validate-jwt header-name="x-zumo-auth" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Supplied access token is invalid.">  
    <issuers>  
        <issuer>urn:microsoft:windows-azure:zumo</issuer>  
    </issuers>  
    <audiences>  
        <audience>Facebook</audience>  
    </audiences>  
    <issuer-signing-keys>  
        <zumo-master-key id="0">insert key here</zumo-master-key>  
    </issuer-signing-keys>  
</validate-jwt>  
```  
  
#### <a name="azure-active-directory-token-validation"></a><span data-ttu-id="be029-378">Azure Active Directory token doğrulama</span><span class="sxs-lookup"><span data-stu-id="be029-378">Azure Active Directory token validation</span></span>  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration" />  
    <audiences>
        <audience>25eef6e4-c905-4a07-8eb4-0d08d5df8b3f</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  

  
#### <a name="azure-active-directory-b2c-token-validation"></a><span data-ttu-id="be029-379">Azure Active Directory B2C belirteç doğrulama</span><span class="sxs-lookup"><span data-stu-id="be029-379">Azure Active Directory B2C token validation</span></span>  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/tfp/contoso.onmicrosoft.com/b2c_1_signin/v2.0/.well-known/openid-configuration" />
    <audiences>
        <audience>d313c4e4-de5f-4197-9470-e509a2f0b806</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  
  
#### <a name="authorize-access-toooperations-based-on-token-claims"></a><span data-ttu-id="be029-380">Belirteç taleplerine dayalı erişim toooperations yetkilendirmek</span><span class="sxs-lookup"><span data-stu-id="be029-380">Authorize access toooperations based on token claims</span></span>  
 <span data-ttu-id="be029-381">Bu örnek gösterir nasıl toouse hello [JWT doğrulamak](api-management-access-restriction-policies.md#ValidateJWT) İlkesi toopre-belirteci taleplerine dayalı erişim toooperations yetkilendirin.</span><span class="sxs-lookup"><span data-stu-id="be029-381">This example shows how toouse hello [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) policy toopre-authorize access toooperations based on token claims.</span></span> <span data-ttu-id="be029-382">Yapılandırma ve bu ilkeyi kullanan bir örnek için bkz: [bulut kapak bölüm 177: daha Vlad Vinogradsky ile yönetim özelliklerini API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) ve too13:50 ileri sarma.</span><span class="sxs-lookup"><span data-stu-id="be029-382">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too13:50.</span></span> <span data-ttu-id="be029-383">Too15:00 hello İlkesi Düzenleyicisi'nde yapılandırılan toosee hello İlkesi sarma ve ardından yetkilendirme belirtecini too18:50 hem ile hem de hello olmadan hello Geliştirici Portalı'ndan bir işlem çağırma, bir örnek için gerekli.</span><span class="sxs-lookup"><span data-stu-id="be029-383">Fast forward too15:00 toosee hello policies configured in hello policy editor and then too18:50 for a demonstration of calling an operation from hello developer portal both with and without hello required authorization token.</span></span>  
  
```xml  
<!-- Copy hello following snippet into hello inbound section at hello api (or higher) level toopre-authorize access toooperations based on token claims -->  
<set-variable name="signingKey" value="insert signing key here" />  
<choose>  
  <when condition="@(context.Request.Method.Equals("patch",StringComparison.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="edit">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <when condition="@(new [] {"post", "put"}.Contains(context.Request.Method,StringComparer.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="create">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <otherwise>  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
    </validate-jwt>  
  </otherwise>  
</choose>  
```  
  
### <a name="elements"></a><span data-ttu-id="be029-384">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="be029-384">Elements</span></span>  
  
|<span data-ttu-id="be029-385">Öğesi</span><span class="sxs-lookup"><span data-stu-id="be029-385">Element</span></span>|<span data-ttu-id="be029-386">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be029-386">Description</span></span>|<span data-ttu-id="be029-387">Gerekli</span><span class="sxs-lookup"><span data-stu-id="be029-387">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="be029-388">doğrulama jwt</span><span class="sxs-lookup"><span data-stu-id="be029-388">validate-jwt</span></span>|<span data-ttu-id="be029-389">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="be029-389">Root element.</span></span>|<span data-ttu-id="be029-390">Evet</span><span class="sxs-lookup"><span data-stu-id="be029-390">Yes</span></span>|  
|<span data-ttu-id="be029-391">Hedef kitle</span><span class="sxs-lookup"><span data-stu-id="be029-391">audiences</span></span>|<span data-ttu-id="be029-392">Merhaba belirteçte mevcut olabilecek kabul edilebilir İzleyici talep listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="be029-392">Contains a list of acceptable audience claims that can be present on hello token.</span></span> <span data-ttu-id="be029-393">Birden fazla hedef kitle değer mevcut sonra her değer denenir kadar tüm (Bu durumda doğrulama başarısız) tükendiği veya biri başarılı olana kadar.</span><span class="sxs-lookup"><span data-stu-id="be029-393">If multiple audience values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span> <span data-ttu-id="be029-394">En az bir hedef kitle belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="be029-394">At least one audience must be specified.</span></span>|<span data-ttu-id="be029-395">Hayır</span><span class="sxs-lookup"><span data-stu-id="be029-395">No</span></span>|  
|<span data-ttu-id="be029-396">verici İmzalama anahtarları</span><span class="sxs-lookup"><span data-stu-id="be029-396">issuer-signing-keys</span></span>|<span data-ttu-id="be029-397">Base64 ile kodlanmış güvenlik kullanılan anahtarları toovalidate listesini belirteçleri imzalanmış.</span><span class="sxs-lookup"><span data-stu-id="be029-397">A list of Base64-encoded security keys used toovalidate signed tokens.</span></span> <span data-ttu-id="be029-398">Birden çok güvenlik anahtarları varsa sonra her anahtar denenir kadar tüm (Bu durumda doğrulama başarısız) tükendiği veya biri (belirteci geçiş işlemi için yararlıdır) başarılı olana kadar.</span><span class="sxs-lookup"><span data-stu-id="be029-398">If multiple security keys are present, then each key is tried until either all are exhausted (in which case validation fails) or until one succeeds (useful for token rollover).</span></span> <span data-ttu-id="be029-399">Anahtar öğeleri sahip isteğe bağlı bir `id` kullanılan öznitelik toomatch karşı `kid` talep.</span><span class="sxs-lookup"><span data-stu-id="be029-399">Key elements have an optional `id` attribute used toomatch against `kid` claim.</span></span>|<span data-ttu-id="be029-400">Hayır</span><span class="sxs-lookup"><span data-stu-id="be029-400">No</span></span>|  
|<span data-ttu-id="be029-401">verenler</span><span class="sxs-lookup"><span data-stu-id="be029-401">issuers</span></span>|<span data-ttu-id="be029-402">Merhaba belirteç kabul edilebilir sorumluların listesini.</span><span class="sxs-lookup"><span data-stu-id="be029-402">A list of acceptable principals that issued hello token.</span></span> <span data-ttu-id="be029-403">Birden çok veren değer mevcut sonra her değer denenir kadar tüm (Bu durumda doğrulama başarısız) tükendiği veya biri başarılı olana kadar.</span><span class="sxs-lookup"><span data-stu-id="be029-403">If multiple issuer values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span>|<span data-ttu-id="be029-404">Hayır</span><span class="sxs-lookup"><span data-stu-id="be029-404">No</span></span>|  
|<span data-ttu-id="be029-405">openıd-config</span><span class="sxs-lookup"><span data-stu-id="be029-405">openid-config</span></span>|<span data-ttu-id="be029-406">içinden İmzalama anahtarları ve veren alınabilir uyumlu bir Open ID yapılandırma endpoint belirtmek için kullanılan hello öğe.</span><span class="sxs-lookup"><span data-stu-id="be029-406">hello element used for specifying a compliant Open ID configuration endpoint from which signing keys and issuer can be obtained.</span></span>|<span data-ttu-id="be029-407">Hayır</span><span class="sxs-lookup"><span data-stu-id="be029-407">No</span></span>|  
|<span data-ttu-id="be029-408">gerekli talep</span><span class="sxs-lookup"><span data-stu-id="be029-408">required-claims</span></span>|<span data-ttu-id="be029-409">Geçerli olarak kabul toobe beklenen talep toobe için hello belirteçte mevcut listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="be029-409">Contains a list of claims expected toobe present on hello token for it toobe considered valid.</span></span> <span data-ttu-id="be029-410">Ne zaman hello `match` özniteliği olarak ayarlanmış çok`all` hello İlkesi'nde her talep değeri için doğrulama toosucceed hello belirteçte mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="be029-410">When hello `match` attribute is set too`all` every claim value in hello policy must be present in hello token for validation toosucceed.</span></span> <span data-ttu-id="be029-411">Ne zaman hello `match` özniteliği olarak ayarlanmış çok`any` en az bir talep doğrulama toosucceed hello belirteçte mevcut olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="be029-411">When hello `match` attribute is set too`any` at least one claim must be present in hello token for validation toosucceed.</span></span>|<span data-ttu-id="be029-412">Hayır</span><span class="sxs-lookup"><span data-stu-id="be029-412">No</span></span>|  
|<span data-ttu-id="be029-413">zumo ana anahtarı</span><span class="sxs-lookup"><span data-stu-id="be029-413">zumo-master-key</span></span>|<span data-ttu-id="be029-414">Ana anahtar için Azure Mobile Services tarafından yayınlanan belirteçleri</span><span class="sxs-lookup"><span data-stu-id="be029-414">Master key for tokens issued by Azure Mobile Services</span></span>|<span data-ttu-id="be029-415">Hayır</span><span class="sxs-lookup"><span data-stu-id="be029-415">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="be029-416">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="be029-416">Attributes</span></span>  
  
|<span data-ttu-id="be029-417">Ad</span><span class="sxs-lookup"><span data-stu-id="be029-417">Name</span></span>|<span data-ttu-id="be029-418">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be029-418">Description</span></span>|<span data-ttu-id="be029-419">Gerekli</span><span class="sxs-lookup"><span data-stu-id="be029-419">Required</span></span>|<span data-ttu-id="be029-420">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="be029-420">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="be029-421">saat eğriltme</span><span class="sxs-lookup"><span data-stu-id="be029-421">clock-skew</span></span>|<span data-ttu-id="be029-422">TimeSpan.</span><span class="sxs-lookup"><span data-stu-id="be029-422">Timespan.</span></span> <span data-ttu-id="be029-423">Merhaba belirtecinin süre sonu talep hello belirteçte ve hello geçerli durumda bazı küçük leeway sağlar tarih / saat.</span><span class="sxs-lookup"><span data-stu-id="be029-423">Provides some small leeway in case hello token's expiration claim is present in hello token and is past hello current date / time.</span></span>|<span data-ttu-id="be029-424">Hayır</span><span class="sxs-lookup"><span data-stu-id="be029-424">No</span></span>|<span data-ttu-id="be029-425">0 saniye</span><span class="sxs-lookup"><span data-stu-id="be029-425">0 seconds</span></span>|  
|<span data-ttu-id="be029-426">başarısız oldu-doğrulama-hata iletisi</span><span class="sxs-lookup"><span data-stu-id="be029-426">failed-validation-error-message</span></span>|<span data-ttu-id="be029-427">Hata iletisi tooreturn hello JWT doğrulamayı geçemezse hello HTTP yanıt gövdesi içinde.</span><span class="sxs-lookup"><span data-stu-id="be029-427">Error message tooreturn in hello HTTP response body if hello JWT does not pass validation.</span></span> <span data-ttu-id="be029-428">Bu ileti, tüm özel karakterleri düzgün şekilde çıkıldığından olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="be029-428">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="be029-429">Hayır</span><span class="sxs-lookup"><span data-stu-id="be029-429">No</span></span>|<span data-ttu-id="be029-430">Varsayılan hata iletisini doğrulama sorunu, örneğin "JWT mevcut değil." bağlıdır</span><span class="sxs-lookup"><span data-stu-id="be029-430">Default error message depends on validation issue, for example "JWT not present."</span></span>|  
|<span data-ttu-id="be029-431">başarısız oldu-doğrulama-httpcode</span><span class="sxs-lookup"><span data-stu-id="be029-431">failed-validation-httpcode</span></span>|<span data-ttu-id="be029-432">HTTP durum kodu tooreturn Hello JWT doğrulamayı geçerse değil.</span><span class="sxs-lookup"><span data-stu-id="be029-432">HTTP Status code tooreturn if hello JWT doesn't pass validation.</span></span>|<span data-ttu-id="be029-433">Hayır</span><span class="sxs-lookup"><span data-stu-id="be029-433">No</span></span>|<span data-ttu-id="be029-434">401</span><span class="sxs-lookup"><span data-stu-id="be029-434">401</span></span>|  
|<span data-ttu-id="be029-435">üstbilgi adı</span><span class="sxs-lookup"><span data-stu-id="be029-435">header-name</span></span>|<span data-ttu-id="be029-436">Merhaba belirteci bulunduran hello HTTP üstbilgisinin Hello adı.</span><span class="sxs-lookup"><span data-stu-id="be029-436">hello name of hello HTTP header holding hello token.</span></span>|<span data-ttu-id="be029-437">Ya da `header-name` veya `query-paremeter-name` belirtilmelidir; ancak ikisi birden değil.</span><span class="sxs-lookup"><span data-stu-id="be029-437">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="be029-438">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-438">N/A</span></span>|  
|<span data-ttu-id="be029-439">id</span><span class="sxs-lookup"><span data-stu-id="be029-439">id</span></span>|<span data-ttu-id="be029-440">Merhaba `id` hello öznitelikte `key` öğesi karşı eşleşen toospecify hello dize verir `kid` hello (varsa) belirteci toofind hello uygun anahtar toouse imza doğrulaması için giden talep.</span><span class="sxs-lookup"><span data-stu-id="be029-440">hello `id` attribute on hello `key` element allows you toospecify hello string that will be matched against `kid` claim in hello token (if present) toofind out hello appropriate key toouse for signature validation.</span></span>|<span data-ttu-id="be029-441">Hayır</span><span class="sxs-lookup"><span data-stu-id="be029-441">No</span></span>|<span data-ttu-id="be029-442">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-442">N/A</span></span>|  
|<span data-ttu-id="be029-443">eşleşme</span><span class="sxs-lookup"><span data-stu-id="be029-443">match</span></span>|<span data-ttu-id="be029-444">Merhaba `match` hello öznitelikte `claim` öğesi hello İlkesi'nde her talep değeri için doğrulama toosucceed hello belirteçte mevcut olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="be029-444">hello `match` attribute on hello `claim` element specifies whether every claim value in hello policy must be present in hello token for validation toosucceed.</span></span> <span data-ttu-id="be029-445">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="be029-445">Possible values are:</span></span><br /><br /> <span data-ttu-id="be029-446">-                          `all`-hello İlkesi'nde her talep değeri için doğrulama toosucceed hello belirteçte mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="be029-446">-                          `all` - every claim value in hello policy must be present in hello token for validation toosucceed.</span></span><br /><br /> <span data-ttu-id="be029-447">-                          `any`-en az bir talep değeri için doğrulama toosucceed hello belirteçte mevcut olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="be029-447">-                          `any` - at least one claim value must be present in hello token for validation toosucceed.</span></span>|<span data-ttu-id="be029-448">Hayır</span><span class="sxs-lookup"><span data-stu-id="be029-448">No</span></span>|<span data-ttu-id="be029-449">Tüm</span><span class="sxs-lookup"><span data-stu-id="be029-449">all</span></span>|  
|<span data-ttu-id="be029-450">Sorgu paremeter adı</span><span class="sxs-lookup"><span data-stu-id="be029-450">query-paremeter-name</span></span>|<span data-ttu-id="be029-451">Merhaba belirteci bulunduran hello hello sorgu parametresi Hello adı.</span><span class="sxs-lookup"><span data-stu-id="be029-451">hello name of hello hello query parameter holding hello token.</span></span>|<span data-ttu-id="be029-452">Ya da `header-name` veya `query-paremeter-name` belirtilmelidir; ancak ikisi birden değil.</span><span class="sxs-lookup"><span data-stu-id="be029-452">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="be029-453">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-453">N/A</span></span>|  
|<span data-ttu-id="be029-454">gerekli-sona erme-time</span><span class="sxs-lookup"><span data-stu-id="be029-454">require-expiration-time</span></span>|<span data-ttu-id="be029-455">Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="be029-455">Boolean.</span></span> <span data-ttu-id="be029-456">Bir süre sonu talep hello belirteçte gerekip gerekmediğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="be029-456">Specifies whether an expiration claim is required in hello token.</span></span>|<span data-ttu-id="be029-457">Hayır</span><span class="sxs-lookup"><span data-stu-id="be029-457">No</span></span>|<span data-ttu-id="be029-458">TRUE</span><span class="sxs-lookup"><span data-stu-id="be029-458">true</span></span>|
|<span data-ttu-id="be029-459">gerektiren düzeni</span><span class="sxs-lookup"><span data-stu-id="be029-459">require-scheme</span></span>|<span data-ttu-id="be029-460">Merhaba belirteci Hello adını düzen, örn. "Bearer".</span><span class="sxs-lookup"><span data-stu-id="be029-460">hello name of hello token scheme, e.g. "Bearer".</span></span> <span data-ttu-id="be029-461">Bu öznitelik ayarlandığında hello İlkesi düzeni hello kimlik doğrulaması üstbilgi değeri mevcut belirtilen güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="be029-461">When this attribute is set, hello policy will ensure that specified scheme is present in hello Authorization header value.</span></span>|<span data-ttu-id="be029-462">Hayır</span><span class="sxs-lookup"><span data-stu-id="be029-462">No</span></span>|<span data-ttu-id="be029-463">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-463">N/A</span></span>|
|<span data-ttu-id="be029-464">gerekli-oturum-belirteçleri</span><span class="sxs-lookup"><span data-stu-id="be029-464">require-signed-tokens</span></span>|<span data-ttu-id="be029-465">Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="be029-465">Boolean.</span></span> <span data-ttu-id="be029-466">Bir belirteç imzalı gerekli toobe olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="be029-466">Specifies whether a token is required toobe signed.</span></span>|<span data-ttu-id="be029-467">Hayır</span><span class="sxs-lookup"><span data-stu-id="be029-467">No</span></span>|<span data-ttu-id="be029-468">TRUE</span><span class="sxs-lookup"><span data-stu-id="be029-468">true</span></span>|  
|<span data-ttu-id="be029-469">URL</span><span class="sxs-lookup"><span data-stu-id="be029-469">url</span></span>|<span data-ttu-id="be029-470">Burada Open ID yapılandırma meta verilerini elde edilebilir gelen kimliği yapılandırma uç noktasının URL'sini açın.</span><span class="sxs-lookup"><span data-stu-id="be029-470">Open ID configuration endpoint URL from where Open ID configuration metadata can be obtained.</span></span> <span data-ttu-id="be029-471">Azure Active Directory için URL aşağıdaki hello kullan: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` directory Kiracı adınız, örneğin değiştirerek `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="be029-471">For Azure Active Directory use hello following URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` substituting your directory tenant name, e.g. `contoso.onmicrosoft.com`.</span></span>|<span data-ttu-id="be029-472">Evet</span><span class="sxs-lookup"><span data-stu-id="be029-472">Yes</span></span>|<span data-ttu-id="be029-473">Yok</span><span class="sxs-lookup"><span data-stu-id="be029-473">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="be029-474">Kullanım</span><span class="sxs-lookup"><span data-stu-id="be029-474">Usage</span></span>  
 <span data-ttu-id="be029-475">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="be029-475">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="be029-476">**İlke bölümleri:** gelen</span><span class="sxs-lookup"><span data-stu-id="be029-476">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="be029-477">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="be029-477">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="be029-478">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="be029-478">Next steps</span></span>
<span data-ttu-id="be029-479">İlkeleriyle çalışma daha fazla bilgi için bkz: [API Management ilkeleri](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="be029-479">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
