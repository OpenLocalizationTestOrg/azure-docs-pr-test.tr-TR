---
title: "Azure API Management erişimi kısıtlama ilkeleri | Microsoft Docs"
description: "Azure API Management'te kullanıma erişim kısıtlama ilkeleri hakkında bilgi edinin."
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
ms.openlocfilehash: 4c9991baf3fbcf3b8ea01f8dd573e2336db88b68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-access-restriction-policies"></a><span data-ttu-id="08845-103">API yönetim erişim kısıtlama ilkeleri</span><span class="sxs-lookup"><span data-stu-id="08845-103">API Management access restriction policies</span></span>
<span data-ttu-id="08845-104">Bu konu aşağıdaki API Management ilkeleri bir başvuru sağlar.</span><span class="sxs-lookup"><span data-stu-id="08845-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="08845-105">Ekleme ve ilkeleri yapılandırma hakkında daha fazla bilgi için bkz: [API Management ilkeleri](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="08845-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="08845-106"><a name="AccessRestrictionPolicies"></a>Erişimi kısıtlama ilkeleri</span><span class="sxs-lookup"><span data-stu-id="08845-106"><a name="AccessRestrictionPolicies"></a> Access restriction policies</span></span>  
  
-   <span data-ttu-id="08845-107">[Onay HTTP üstbilgisi](api-management-access-restriction-policies.md#CheckHTTPHeader) -varlığı ve/veya bir HTTP üstbilgisi değerini zorlar.</span><span class="sxs-lookup"><span data-stu-id="08845-107">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
-   <span data-ttu-id="08845-108">[Abonelik tarafından çağrı hızını sınırla](api-management-access-restriction-policies.md#LimitCallRate) -engeller API kullanımı ani başına abonelik başına çağrı hızını sınırlayarak.</span><span class="sxs-lookup"><span data-stu-id="08845-108">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="08845-109">[Anahtara göre çağrı hızını sınırla](#LimitCallRateByKey) -engeller API kullanımı ani başına anahtar başına çağrı hızını sınırlayarak.</span><span class="sxs-lookup"><span data-stu-id="08845-109">[Limit call rate by key](#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
-   <span data-ttu-id="08845-110">[Arayan IP'leri kısıtlamak](api-management-access-restriction-policies.md#RestrictCallerIPs) -filtreleri (verir/engellediği) çağrılarından belirli IP adreslerini ve/veya adres aralığı.</span><span class="sxs-lookup"><span data-stu-id="08845-110">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
-   <span data-ttu-id="08845-111">[Abonelik tarafından kullanım kotası ayarla](api-management-access-restriction-policies.md#SetUsageQuota) -yenilenebilir veya ömrü çağrısı birim ve/veya bant genişliği kota, abonelik başına temelinde zorunlu tutmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="08845-111">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="08845-112">[Anahtara göre kullanım kotası ayarla](#SetUsageQuotaByKey) -yenilenebilir veya ömrü çağrısı birim ve/veya bant genişliği kota anahtarı başına temelinde zorunlu tutmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="08845-112">[Set usage quota by key](#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
-   <span data-ttu-id="08845-113">[JWT doğrulama](api-management-access-restriction-policies.md#ValidateJWT) -varlığı ve belirtilen bir HTTP üstbilgisi veya belirtilen sorgu parametresi ayıklanan JWT geçerliliğini zorlar.</span><span class="sxs-lookup"><span data-stu-id="08845-113">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
##  <span data-ttu-id="08845-114"><a name="CheckHTTPHeader"></a>HTTP üstbilgisi denetleyin</span><span class="sxs-lookup"><span data-stu-id="08845-114"><a name="CheckHTTPHeader"></a> Check HTTP header</span></span>  
 <span data-ttu-id="08845-115">Kullanım `check-header` bir istek belirtilen bir HTTP üstbilgisi olduğunu zorlamak için ilke.</span><span class="sxs-lookup"><span data-stu-id="08845-115">Use the `check-header` policy to enforce that a request has a specified HTTP header.</span></span> <span data-ttu-id="08845-116">İsteğe bağlı olarak üstbilgi belirli bir değer veya izin verilen değer aralığı için onay olup olmadığını görmek için kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08845-116">You can optionally check to see if the header has a specific value or check for a range of allowed values.</span></span> <span data-ttu-id="08845-117">Denetimi başarısız olursa, ilke isteği işleme sonlandırır ve ilke tarafından belirtilen HTTP durum kodu ve hata iletisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="08845-117">If the check fails, the policy terminates request processing and returns the HTTP status code and error message specified by the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="08845-118">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="08845-118">Policy statement</span></span>  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a><span data-ttu-id="08845-119">Örnek</span><span class="sxs-lookup"><span data-stu-id="08845-119">Example</span></span>  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a><span data-ttu-id="08845-120">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="08845-120">Elements</span></span>  
  
|<span data-ttu-id="08845-121">Ad</span><span class="sxs-lookup"><span data-stu-id="08845-121">Name</span></span>|<span data-ttu-id="08845-122">Açıklama</span><span class="sxs-lookup"><span data-stu-id="08845-122">Description</span></span>|<span data-ttu-id="08845-123">Gerekli</span><span class="sxs-lookup"><span data-stu-id="08845-123">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="08845-124">onay üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="08845-124">check-header</span></span>|<span data-ttu-id="08845-125">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="08845-125">Root element.</span></span>|<span data-ttu-id="08845-126">Evet</span><span class="sxs-lookup"><span data-stu-id="08845-126">Yes</span></span>|  
|<span data-ttu-id="08845-127">değer</span><span class="sxs-lookup"><span data-stu-id="08845-127">value</span></span>|<span data-ttu-id="08845-128">İzin verilen HTTP üstbilgisi değeri.</span><span class="sxs-lookup"><span data-stu-id="08845-128">Allowed HTTP header value.</span></span> <span data-ttu-id="08845-129">Birden çok değer öğesi belirtildiğinde değerlerden herhangi biri bir eşleşme varsa onay başarı olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="08845-129">When multiple value elements are specified, the check is considered a success if any one of the values is a match.</span></span>|<span data-ttu-id="08845-130">Hayır</span><span class="sxs-lookup"><span data-stu-id="08845-130">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="08845-131">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="08845-131">Attributes</span></span>  
  
|<span data-ttu-id="08845-132">Ad</span><span class="sxs-lookup"><span data-stu-id="08845-132">Name</span></span>|<span data-ttu-id="08845-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="08845-133">Description</span></span>|<span data-ttu-id="08845-134">Gerekli</span><span class="sxs-lookup"><span data-stu-id="08845-134">Required</span></span>|<span data-ttu-id="08845-135">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="08845-135">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="08845-136">başarısız oldu-onay-hata iletisi</span><span class="sxs-lookup"><span data-stu-id="08845-136">failed-check-error-message</span></span>|<span data-ttu-id="08845-137">HTTP yanıt gövdesinde başlığı yok veya geçersiz bir değere sahip ise döndürülecek hata iletisi.</span><span class="sxs-lookup"><span data-stu-id="08845-137">Error message to return in the HTTP response body if the header doesn't exist or has an invalid value.</span></span> <span data-ttu-id="08845-138">Bu ileti, tüm özel karakterleri düzgün şekilde çıkıldığından olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="08845-138">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="08845-139">Evet</span><span class="sxs-lookup"><span data-stu-id="08845-139">Yes</span></span>|<span data-ttu-id="08845-140">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-140">N/A</span></span>|  
|<span data-ttu-id="08845-141">başarısız oldu-onay-httpcode</span><span class="sxs-lookup"><span data-stu-id="08845-141">failed-check-httpcode</span></span>|<span data-ttu-id="08845-142">Üstbilgi yok veya geçersiz bir değere sahip olursa döndürmek için HTTP durum kodu.</span><span class="sxs-lookup"><span data-stu-id="08845-142">HTTP Status code to return if the header doesn't exist or has an invalid value.</span></span>|<span data-ttu-id="08845-143">Evet</span><span class="sxs-lookup"><span data-stu-id="08845-143">Yes</span></span>|<span data-ttu-id="08845-144">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-144">N/A</span></span>|  
|<span data-ttu-id="08845-145">üstbilgi adı</span><span class="sxs-lookup"><span data-stu-id="08845-145">header-name</span></span>|<span data-ttu-id="08845-146">Denetlenecek HTTP üstbilgisinin adı.</span><span class="sxs-lookup"><span data-stu-id="08845-146">The name of the HTTP Header to check.</span></span>|<span data-ttu-id="08845-147">Evet</span><span class="sxs-lookup"><span data-stu-id="08845-147">Yes</span></span>|<span data-ttu-id="08845-148">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-148">N/A</span></span>|  
|<span data-ttu-id="08845-149">Yoksay durumu</span><span class="sxs-lookup"><span data-stu-id="08845-149">ignore-case</span></span>|<span data-ttu-id="08845-150">TRUE veya False ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="08845-150">Can be set to True or False.</span></span> <span data-ttu-id="08845-151">Üstbilgi değeri kabul edilebilir değerler kümesi karşı karşılaştırıldığında doğru servis talebi kümesine göz ardı gerekiyorsa.</span><span class="sxs-lookup"><span data-stu-id="08845-151">If set to True case is ignored when the header value is compared against the set of acceptable values.</span></span>|<span data-ttu-id="08845-152">Evet</span><span class="sxs-lookup"><span data-stu-id="08845-152">Yes</span></span>|<span data-ttu-id="08845-153">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-153">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="08845-154">Kullanım</span><span class="sxs-lookup"><span data-stu-id="08845-154">Usage</span></span>  
 <span data-ttu-id="08845-155">Bu ilke aşağıdaki ilkesi kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="08845-155">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="08845-156">**İlke bölümleri:** gelen, giden</span><span class="sxs-lookup"><span data-stu-id="08845-156">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="08845-157">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="08845-157">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="08845-158"><a name="LimitCallRate"></a>Abonelik tarafından çağrı hızını sınırla</span><span class="sxs-lookup"><span data-stu-id="08845-158"><a name="LimitCallRate"></a> Limit call rate by subscription</span></span>  
 <span data-ttu-id="08845-159">`rate-limit` İlke sayıyı belirtilen sayıda belirli bir süre başına çağrı hızını sınırlayarak API kullanımındaki ani bir abonelik başına temelinde engeller.</span><span class="sxs-lookup"><span data-stu-id="08845-159">The `rate-limit` policy prevents API usage spikes on a per subscription basis by limiting the call rate to a specified number per a specified time period.</span></span> <span data-ttu-id="08845-160">Bu ilke tetiklendiğinde arayan alan bir `429 Too Many Requests` yanıt durum kodu.</span><span class="sxs-lookup"><span data-stu-id="08845-160">When this policy is triggered the caller receives a `429 Too Many Requests` response status code.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="08845-161">Bu ilke, ilke belge başına yalnızca bir kez kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="08845-161">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="08845-162">[İlke ifadeleri](api-management-policy-expressions.md) İlkesi özniteliklerini hiçbirinde Bu ilke için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="08845-162">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="08845-163">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="08845-163">Policy statement</span></span>  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a><span data-ttu-id="08845-164">Örnek</span><span class="sxs-lookup"><span data-stu-id="08845-164">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="08845-165">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="08845-165">Elements</span></span>  
  
|<span data-ttu-id="08845-166">Ad</span><span class="sxs-lookup"><span data-stu-id="08845-166">Name</span></span>|<span data-ttu-id="08845-167">Açıklama</span><span class="sxs-lookup"><span data-stu-id="08845-167">Description</span></span>|<span data-ttu-id="08845-168">Gerekli</span><span class="sxs-lookup"><span data-stu-id="08845-168">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="08845-169">sınırını ayarlama</span><span class="sxs-lookup"><span data-stu-id="08845-169">set-limit</span></span>|<span data-ttu-id="08845-170">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="08845-170">Root element.</span></span>|<span data-ttu-id="08845-171">Evet</span><span class="sxs-lookup"><span data-stu-id="08845-171">Yes</span></span>|  
|<span data-ttu-id="08845-172">api</span><span class="sxs-lookup"><span data-stu-id="08845-172">api</span></span>|<span data-ttu-id="08845-173">Bir veya daha fazla ürün içinde çağrı hızı sınırı üzerinde API'leri zorunlu tuttukları için bu öğeleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="08845-173">Add one  or more of these elements to impose a call rate limit on APIs within the product.</span></span> <span data-ttu-id="08845-174">Ürün ve API sınırları bağımsız olarak uygulanır oranı arayın.</span><span class="sxs-lookup"><span data-stu-id="08845-174">Product and API call rate limits are applied independently.</span></span>|<span data-ttu-id="08845-175">Hayır</span><span class="sxs-lookup"><span data-stu-id="08845-175">No</span></span>|  
|<span data-ttu-id="08845-176">işlemi</span><span class="sxs-lookup"><span data-stu-id="08845-176">operation</span></span>|<span data-ttu-id="08845-177">Bir veya daha fazla bir API işlemlerini bir çağrı hızı sınırı koymak için bu öğeleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="08845-177">Add one  or more of these elements to impose a call rate limit on operations within an API.</span></span> <span data-ttu-id="08845-178">Ürün, API ve işlem sınırları bağımsız olarak uygulanır oranı çağırın.</span><span class="sxs-lookup"><span data-stu-id="08845-178">Product, API, and operation call rate limits are applied independently.</span></span>|<span data-ttu-id="08845-179">Hayır</span><span class="sxs-lookup"><span data-stu-id="08845-179">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="08845-180">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="08845-180">Attributes</span></span>  
  
|<span data-ttu-id="08845-181">Ad</span><span class="sxs-lookup"><span data-stu-id="08845-181">Name</span></span>|<span data-ttu-id="08845-182">Açıklama</span><span class="sxs-lookup"><span data-stu-id="08845-182">Description</span></span>|<span data-ttu-id="08845-183">Gerekli</span><span class="sxs-lookup"><span data-stu-id="08845-183">Required</span></span>|<span data-ttu-id="08845-184">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="08845-184">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="08845-185">ad</span><span class="sxs-lookup"><span data-stu-id="08845-185">name</span></span>|<span data-ttu-id="08845-186">Hız sınırı uygulanacağı için API adı.</span><span class="sxs-lookup"><span data-stu-id="08845-186">The name of the API for which to apply the rate limit.</span></span>|<span data-ttu-id="08845-187">Evet</span><span class="sxs-lookup"><span data-stu-id="08845-187">Yes</span></span>|<span data-ttu-id="08845-188">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-188">N/A</span></span>|  
|<span data-ttu-id="08845-189">çağrıları</span><span class="sxs-lookup"><span data-stu-id="08845-189">calls</span></span>|<span data-ttu-id="08845-190">Çağrı belirtilen zaman aralığı boyunca izin verilen en fazla toplam sayısı `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="08845-190">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="08845-191">Evet</span><span class="sxs-lookup"><span data-stu-id="08845-191">Yes</span></span>|<span data-ttu-id="08845-192">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-192">N/A</span></span>|  
|<span data-ttu-id="08845-193">yenileme dönemi</span><span class="sxs-lookup"><span data-stu-id="08845-193">renewal-period</span></span>|<span data-ttu-id="08845-194">Zaman aralığını saniye olarak geçmesi kota sıfırlar.</span><span class="sxs-lookup"><span data-stu-id="08845-194">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="08845-195">Evet</span><span class="sxs-lookup"><span data-stu-id="08845-195">Yes</span></span>|<span data-ttu-id="08845-196">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-196">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="08845-197">Kullanım</span><span class="sxs-lookup"><span data-stu-id="08845-197">Usage</span></span>  
 <span data-ttu-id="08845-198">Bu ilke aşağıdaki ilkesi kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="08845-198">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="08845-199">**İlke bölümleri:** gelen</span><span class="sxs-lookup"><span data-stu-id="08845-199">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="08845-200">**İlke kapsamları:** ürün</span><span class="sxs-lookup"><span data-stu-id="08845-200">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="08845-201"><a name="LimitCallRateByKey"></a>Anahtara göre çağrı hızını sınırla</span><span class="sxs-lookup"><span data-stu-id="08845-201"><a name="LimitCallRateByKey"></a> Limit call rate by key</span></span>  
 <span data-ttu-id="08845-202">`rate-limit-by-key` İlke sayıyı belirtilen sayıda belirli bir süre başına çağrı hızını sınırlayarak API kullanımındaki ani bir anahtar başına temelinde engeller.</span><span class="sxs-lookup"><span data-stu-id="08845-202">The `rate-limit-by-key` policy prevents API usage spikes on a per key basis by limiting the call rate to a specified number per a specified time period.</span></span> <span data-ttu-id="08845-203">Anahtar isteğe bağlı bir dize değerine sahip olabilir ve genellikle bir ilke ifade kullanılarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="08845-203">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="08845-204">İsteğe bağlı increment koşulu, hangi isteklerinin sınırında sayılır belirtmek için eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="08845-204">Optional increment condition can be added to specify which requests should be counted towards the limit.</span></span> <span data-ttu-id="08845-205">Bu ilke tetiklendiğinde arayan alan bir `429 Too Many Requests` yanıt durum kodu.</span><span class="sxs-lookup"><span data-stu-id="08845-205">When this policy is triggered the caller receives a `429 Too Many Requests` response status code.</span></span>  
  
 <span data-ttu-id="08845-206">Daha fazla bilgi ve bu ilkeyi örnekleri için bkz: [Gelişmiş istek azaltma Azure API Management ile](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="08845-206">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="08845-207">Bu ilke, ilke belge başına yalnızca bir kez kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="08845-207">This policy can be used only once per policy document.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="08845-208">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="08845-208">Policy statement</span></span>  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="08845-209">Örnek</span><span class="sxs-lookup"><span data-stu-id="08845-209">Example</span></span>  
 <span data-ttu-id="08845-210">Aşağıdaki örnekte, hız sınırı arayan IP adresine göre anahtarlanır.</span><span class="sxs-lookup"><span data-stu-id="08845-210">In the following example, the rate limit is keyed by the caller IP address.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="08845-211">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="08845-211">Elements</span></span>  
  
|<span data-ttu-id="08845-212">Ad</span><span class="sxs-lookup"><span data-stu-id="08845-212">Name</span></span>|<span data-ttu-id="08845-213">Açıklama</span><span class="sxs-lookup"><span data-stu-id="08845-213">Description</span></span>|<span data-ttu-id="08845-214">Gerekli</span><span class="sxs-lookup"><span data-stu-id="08845-214">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="08845-215">sınırını ayarlama</span><span class="sxs-lookup"><span data-stu-id="08845-215">set-limit</span></span>|<span data-ttu-id="08845-216">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="08845-216">Root element.</span></span>|<span data-ttu-id="08845-217">Evet</span><span class="sxs-lookup"><span data-stu-id="08845-217">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="08845-218">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="08845-218">Attributes</span></span>  
  
|<span data-ttu-id="08845-219">Ad</span><span class="sxs-lookup"><span data-stu-id="08845-219">Name</span></span>|<span data-ttu-id="08845-220">Açıklama</span><span class="sxs-lookup"><span data-stu-id="08845-220">Description</span></span>|<span data-ttu-id="08845-221">Gerekli</span><span class="sxs-lookup"><span data-stu-id="08845-221">Required</span></span>|<span data-ttu-id="08845-222">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="08845-222">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="08845-223">çağrıları</span><span class="sxs-lookup"><span data-stu-id="08845-223">calls</span></span>|<span data-ttu-id="08845-224">Çağrı belirtilen zaman aralığı boyunca izin verilen en fazla toplam sayısı `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="08845-224">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="08845-225">Evet</span><span class="sxs-lookup"><span data-stu-id="08845-225">Yes</span></span>|<span data-ttu-id="08845-226">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-226">N/A</span></span>|  
|<span data-ttu-id="08845-227">Tamamlayıcı anahtarı</span><span class="sxs-lookup"><span data-stu-id="08845-227">counter-key</span></span>|<span data-ttu-id="08845-228">Hız sınırı ilkesi için kullanılacak anahtarı.</span><span class="sxs-lookup"><span data-stu-id="08845-228">The key to use for the rate limit policy.</span></span>|<span data-ttu-id="08845-229">Evet</span><span class="sxs-lookup"><span data-stu-id="08845-229">Yes</span></span>|<span data-ttu-id="08845-230">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-230">N/A</span></span>|  
|<span data-ttu-id="08845-231">Koşul artırma</span><span class="sxs-lookup"><span data-stu-id="08845-231">increment-condition</span></span>|<span data-ttu-id="08845-232">İstek kota sayılan varsa belirten boolean ifadesi (`true`).</span><span class="sxs-lookup"><span data-stu-id="08845-232">The boolean expression specifying if the request should be counted towards the quota (`true`).</span></span>|<span data-ttu-id="08845-233">Hayır</span><span class="sxs-lookup"><span data-stu-id="08845-233">No</span></span>|<span data-ttu-id="08845-234">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-234">N/A</span></span>|  
|<span data-ttu-id="08845-235">yenileme dönemi</span><span class="sxs-lookup"><span data-stu-id="08845-235">renewal-period</span></span>|<span data-ttu-id="08845-236">Zaman aralığını saniye olarak geçmesi kota sıfırlar.</span><span class="sxs-lookup"><span data-stu-id="08845-236">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="08845-237">Evet</span><span class="sxs-lookup"><span data-stu-id="08845-237">Yes</span></span>|<span data-ttu-id="08845-238">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-238">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="08845-239">Kullanım</span><span class="sxs-lookup"><span data-stu-id="08845-239">Usage</span></span>  
 <span data-ttu-id="08845-240">Bu ilke aşağıdaki ilkesi kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="08845-240">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="08845-241">**İlke bölümleri:** gelen</span><span class="sxs-lookup"><span data-stu-id="08845-241">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="08845-242">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="08845-242">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="08845-243"><a name="RestrictCallerIPs"></a>Arayan IP'leri kısıtla</span><span class="sxs-lookup"><span data-stu-id="08845-243"><a name="RestrictCallerIPs"></a> Restrict caller IPs</span></span>  
 <span data-ttu-id="08845-244">`ip-filter` İlke filtrelerini belirli IP adreslerini ve/veya adres aralıklarını gelen çağrıları (verir/engeller).</span><span class="sxs-lookup"><span data-stu-id="08845-244">The `ip-filter` policy filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="08845-245">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="08845-245">Policy statement</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a><span data-ttu-id="08845-246">Örnek</span><span class="sxs-lookup"><span data-stu-id="08845-246">Example</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a><span data-ttu-id="08845-247">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="08845-247">Elements</span></span>  
  
|<span data-ttu-id="08845-248">Ad</span><span class="sxs-lookup"><span data-stu-id="08845-248">Name</span></span>|<span data-ttu-id="08845-249">Açıklama</span><span class="sxs-lookup"><span data-stu-id="08845-249">Description</span></span>|<span data-ttu-id="08845-250">Gerekli</span><span class="sxs-lookup"><span data-stu-id="08845-250">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="08845-251">IP Filtresi</span><span class="sxs-lookup"><span data-stu-id="08845-251">ip-filter</span></span>|<span data-ttu-id="08845-252">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="08845-252">Root element.</span></span>|<span data-ttu-id="08845-253">Evet</span><span class="sxs-lookup"><span data-stu-id="08845-253">Yes</span></span>|  
|<span data-ttu-id="08845-254">Adres</span><span class="sxs-lookup"><span data-stu-id="08845-254">address</span></span>|<span data-ttu-id="08845-255">Filtre uygulamak tek bir IP adresini belirtir.</span><span class="sxs-lookup"><span data-stu-id="08845-255">Specifies a single IP address on which to filter.</span></span>|<span data-ttu-id="08845-256">En az bir `address` veya `address-range` öğesi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="08845-256">At least one `address` or `address-range` element is required.</span></span>|  
|<span data-ttu-id="08845-257">adres aralığı adresinden ="" için "Adres" =</span><span class="sxs-lookup"><span data-stu-id="08845-257">address-range from="address" to="address"</span></span>|<span data-ttu-id="08845-258">Bir IP adresi aralığı filtrelemek için belirtir.</span><span class="sxs-lookup"><span data-stu-id="08845-258">Specifies a range of IP address on which to filter.</span></span>|<span data-ttu-id="08845-259">En az bir `address` veya `address-range` öğesi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="08845-259">At least one `address` or `address-range` element is required.</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="08845-260">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="08845-260">Attributes</span></span>  
  
|<span data-ttu-id="08845-261">Ad</span><span class="sxs-lookup"><span data-stu-id="08845-261">Name</span></span>|<span data-ttu-id="08845-262">Açıklama</span><span class="sxs-lookup"><span data-stu-id="08845-262">Description</span></span>|<span data-ttu-id="08845-263">Gerekli</span><span class="sxs-lookup"><span data-stu-id="08845-263">Required</span></span>|<span data-ttu-id="08845-264">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="08845-264">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="08845-265">adres aralığı adresinden ="" için "Adres" =</span><span class="sxs-lookup"><span data-stu-id="08845-265">address-range from="address" to="address"</span></span>|<span data-ttu-id="08845-266">Bir dizi IP adreslerini izin vermek veya erişimi reddetmek için.</span><span class="sxs-lookup"><span data-stu-id="08845-266">A range of IP addresses to allow or deny access for.</span></span>|<span data-ttu-id="08845-267">Ne zaman gerekli `address-range` öğe kullanılır.</span><span class="sxs-lookup"><span data-stu-id="08845-267">Required when the `address-range` element is used.</span></span>|<span data-ttu-id="08845-268">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-268">N/A</span></span>|  
|<span data-ttu-id="08845-269">IP filtre eylemi = "izin &#124; yasaklamaz"</span><span class="sxs-lookup"><span data-stu-id="08845-269">ip-filter action="allow &#124; forbid"</span></span>|<span data-ttu-id="08845-270">Çağrıları verilip verilmeyeceğini veya belirtilen IP adresleri ve aralıkları için belirtir.</span><span class="sxs-lookup"><span data-stu-id="08845-270">Specifies whether calls should be allowed or not for the specified IP addresses and ranges.</span></span>|<span data-ttu-id="08845-271">Evet</span><span class="sxs-lookup"><span data-stu-id="08845-271">Yes</span></span>|<span data-ttu-id="08845-272">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="08845-273">Kullanım</span><span class="sxs-lookup"><span data-stu-id="08845-273">Usage</span></span>  
 <span data-ttu-id="08845-274">Bu ilke aşağıdaki ilkesi kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="08845-274">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="08845-275">**İlke bölümleri:** gelen</span><span class="sxs-lookup"><span data-stu-id="08845-275">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="08845-276">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="08845-276">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="08845-277"><a name="SetUsageQuota"></a>Abonelik tarafından kullanım kotası ayarla</span><span class="sxs-lookup"><span data-stu-id="08845-277"><a name="SetUsageQuota"></a> Set usage quota by subscription</span></span>  
 <span data-ttu-id="08845-278">`quota` İlke yenilenebilir veya ömrü çağrısı birim ve/veya bant genişliği kota, abonelik başına temelinde zorunlu tutar.</span><span class="sxs-lookup"><span data-stu-id="08845-278">The `quota` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="08845-279">Bu ilke, ilke belge başına yalnızca bir kez kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="08845-279">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="08845-280">[İlke ifadeleri](api-management-policy-expressions.md) İlkesi özniteliklerini hiçbirinde Bu ilke için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="08845-280">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="08845-281">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="08845-281">Policy statement</span></span>  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a><span data-ttu-id="08845-282">Örnek</span><span class="sxs-lookup"><span data-stu-id="08845-282">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="08845-283">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="08845-283">Elements</span></span>  
  
|<span data-ttu-id="08845-284">Ad</span><span class="sxs-lookup"><span data-stu-id="08845-284">Name</span></span>|<span data-ttu-id="08845-285">Açıklama</span><span class="sxs-lookup"><span data-stu-id="08845-285">Description</span></span>|<span data-ttu-id="08845-286">Gerekli</span><span class="sxs-lookup"><span data-stu-id="08845-286">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="08845-287">Kota</span><span class="sxs-lookup"><span data-stu-id="08845-287">quota</span></span>|<span data-ttu-id="08845-288">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="08845-288">Root element.</span></span>|<span data-ttu-id="08845-289">Evet</span><span class="sxs-lookup"><span data-stu-id="08845-289">Yes</span></span>|  
|<span data-ttu-id="08845-290">api</span><span class="sxs-lookup"><span data-stu-id="08845-290">api</span></span>|<span data-ttu-id="08845-291">Bir veya daha fazla API'lerde kota ürün içinde koymak için bu öğeleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="08845-291">Add one  or more of these elements to impose a quota on APIs within the product.</span></span> <span data-ttu-id="08845-292">Ürün ve API kotaları bağımsız olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="08845-292">Product and API quotas are applied independently.</span></span>|<span data-ttu-id="08845-293">Hayır</span><span class="sxs-lookup"><span data-stu-id="08845-293">No</span></span>|  
|<span data-ttu-id="08845-294">işlemi</span><span class="sxs-lookup"><span data-stu-id="08845-294">operation</span></span>|<span data-ttu-id="08845-295">Bir veya daha fazla bir API işlemlerini bir kota koymak için bu öğeleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="08845-295">Add one  or more of these elements to impose a quota on operations within an API.</span></span> <span data-ttu-id="08845-296">Ürün, API ve işlem kotaları bağımsız olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="08845-296">Product, API, and operation quotas are applied independently.</span></span>|<span data-ttu-id="08845-297">Hayır</span><span class="sxs-lookup"><span data-stu-id="08845-297">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="08845-298">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="08845-298">Attributes</span></span>  
  
|<span data-ttu-id="08845-299">Ad</span><span class="sxs-lookup"><span data-stu-id="08845-299">Name</span></span>|<span data-ttu-id="08845-300">Açıklama</span><span class="sxs-lookup"><span data-stu-id="08845-300">Description</span></span>|<span data-ttu-id="08845-301">Gerekli</span><span class="sxs-lookup"><span data-stu-id="08845-301">Required</span></span>|<span data-ttu-id="08845-302">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="08845-302">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="08845-303">ad</span><span class="sxs-lookup"><span data-stu-id="08845-303">name</span></span>|<span data-ttu-id="08845-304">API veya adını kota uygulandığı işlemi.</span><span class="sxs-lookup"><span data-stu-id="08845-304">The name of the API or operation for which the quota applies.</span></span>|<span data-ttu-id="08845-305">Evet</span><span class="sxs-lookup"><span data-stu-id="08845-305">Yes</span></span>|<span data-ttu-id="08845-306">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-306">N/A</span></span>|  
|<span data-ttu-id="08845-307">Bant genişliği</span><span class="sxs-lookup"><span data-stu-id="08845-307">bandwidth</span></span>|<span data-ttu-id="08845-308">Kilobayt belirtilen zaman aralığı boyunca izin verilen en fazla toplam sayısı `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="08845-308">The maximum total number of kilobytes allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="08845-309">Her iki `calls`, `bandwidth`, veya her ikisini de birlikte belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="08845-309">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="08845-310">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-310">N/A</span></span>|  
|<span data-ttu-id="08845-311">çağrıları</span><span class="sxs-lookup"><span data-stu-id="08845-311">calls</span></span>|<span data-ttu-id="08845-312">Çağrı belirtilen zaman aralığı boyunca izin verilen en fazla toplam sayısı `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="08845-312">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="08845-313">Her iki `calls`, `bandwidth`, veya her ikisini de birlikte belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="08845-313">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="08845-314">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-314">N/A</span></span>|  
|<span data-ttu-id="08845-315">yenileme dönemi</span><span class="sxs-lookup"><span data-stu-id="08845-315">renewal-period</span></span>|<span data-ttu-id="08845-316">Zaman aralığını saniye olarak geçmesi kota sıfırlar.</span><span class="sxs-lookup"><span data-stu-id="08845-316">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="08845-317">Evet</span><span class="sxs-lookup"><span data-stu-id="08845-317">Yes</span></span>|<span data-ttu-id="08845-318">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-318">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="08845-319">Kullanım</span><span class="sxs-lookup"><span data-stu-id="08845-319">Usage</span></span>  
 <span data-ttu-id="08845-320">Bu ilke aşağıdaki ilkesi kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="08845-320">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="08845-321">**İlke bölümleri:** gelen</span><span class="sxs-lookup"><span data-stu-id="08845-321">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="08845-322">**İlke kapsamları:** ürün</span><span class="sxs-lookup"><span data-stu-id="08845-322">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="08845-323"><a name="SetUsageQuotaByKey"></a>Anahtara göre kullanım kotası ayarla</span><span class="sxs-lookup"><span data-stu-id="08845-323"><a name="SetUsageQuotaByKey"></a> Set usage quota by key</span></span>  
 <span data-ttu-id="08845-324">`quota-by-key` İlke yenilenebilir veya ömrü çağrısı birim ve/veya bant genişliği kota anahtarı başına temelinde zorunlu tutar.</span><span class="sxs-lookup"><span data-stu-id="08845-324">The `quota-by-key` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span> <span data-ttu-id="08845-325">Anahtar isteğe bağlı bir dize değerine sahip olabilir ve genellikle bir ilke ifade kullanılarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="08845-325">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="08845-326">İsteğe bağlı increment koşulu, hangi istekler kota sayılması belirtmek için eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="08845-326">Optional increment condition can be added to specify which requests should be counted towards the quota.</span></span>  
  
 <span data-ttu-id="08845-327">Daha fazla bilgi ve bu ilkeyi örnekleri için bkz: [Gelişmiş istek azaltma Azure API Management ile](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="08845-327">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="08845-328">Bu ilke, ilke belge başına yalnızca bir kez kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="08845-328">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="08845-329">[İlke ifadeleri](api-management-policy-expressions.md) İlkesi özniteliklerini hiçbirinde Bu ilke için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="08845-329">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="08845-330">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="08845-330">Policy statement</span></span>  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="08845-331">Örnek</span><span class="sxs-lookup"><span data-stu-id="08845-331">Example</span></span>  
 <span data-ttu-id="08845-332">Aşağıdaki örnekte, kota arayan IP adresine göre anahtarlanır.</span><span class="sxs-lookup"><span data-stu-id="08845-332">In the following example, the quota is keyed by the caller IP address.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="08845-333">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="08845-333">Elements</span></span>  
  
|<span data-ttu-id="08845-334">Ad</span><span class="sxs-lookup"><span data-stu-id="08845-334">Name</span></span>|<span data-ttu-id="08845-335">Açıklama</span><span class="sxs-lookup"><span data-stu-id="08845-335">Description</span></span>|<span data-ttu-id="08845-336">Gerekli</span><span class="sxs-lookup"><span data-stu-id="08845-336">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="08845-337">Kota</span><span class="sxs-lookup"><span data-stu-id="08845-337">quota</span></span>|<span data-ttu-id="08845-338">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="08845-338">Root element.</span></span>|<span data-ttu-id="08845-339">Evet</span><span class="sxs-lookup"><span data-stu-id="08845-339">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="08845-340">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="08845-340">Attributes</span></span>  
  
|<span data-ttu-id="08845-341">Ad</span><span class="sxs-lookup"><span data-stu-id="08845-341">Name</span></span>|<span data-ttu-id="08845-342">Açıklama</span><span class="sxs-lookup"><span data-stu-id="08845-342">Description</span></span>|<span data-ttu-id="08845-343">Gerekli</span><span class="sxs-lookup"><span data-stu-id="08845-343">Required</span></span>|<span data-ttu-id="08845-344">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="08845-344">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="08845-345">Bant genişliği</span><span class="sxs-lookup"><span data-stu-id="08845-345">bandwidth</span></span>|<span data-ttu-id="08845-346">Kilobayt belirtilen zaman aralığı boyunca izin verilen en fazla toplam sayısı `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="08845-346">The maximum total number of kilobytes allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="08845-347">Her iki `calls`, `bandwidth`, veya her ikisini de birlikte belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="08845-347">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="08845-348">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-348">N/A</span></span>|  
|<span data-ttu-id="08845-349">çağrıları</span><span class="sxs-lookup"><span data-stu-id="08845-349">calls</span></span>|<span data-ttu-id="08845-350">Çağrı belirtilen zaman aralığı boyunca izin verilen en fazla toplam sayısı `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="08845-350">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="08845-351">Her iki `calls`, `bandwidth`, veya her ikisini de birlikte belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="08845-351">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="08845-352">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-352">N/A</span></span>|  
|<span data-ttu-id="08845-353">Tamamlayıcı anahtarı</span><span class="sxs-lookup"><span data-stu-id="08845-353">counter-key</span></span>|<span data-ttu-id="08845-354">Kota ilkesi için kullanılacak anahtarı.</span><span class="sxs-lookup"><span data-stu-id="08845-354">The key to use for the quota policy.</span></span>|<span data-ttu-id="08845-355">Evet</span><span class="sxs-lookup"><span data-stu-id="08845-355">Yes</span></span>|<span data-ttu-id="08845-356">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-356">N/A</span></span>|  
|<span data-ttu-id="08845-357">Koşul artırma</span><span class="sxs-lookup"><span data-stu-id="08845-357">increment-condition</span></span>|<span data-ttu-id="08845-358">İstek kota sayılan varsa belirten boolean ifadesi (`true`)</span><span class="sxs-lookup"><span data-stu-id="08845-358">The boolean expression specifying if the request should be counted towards the quota (`true`)</span></span>|<span data-ttu-id="08845-359">Hayır</span><span class="sxs-lookup"><span data-stu-id="08845-359">No</span></span>|<span data-ttu-id="08845-360">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-360">N/A</span></span>|  
|<span data-ttu-id="08845-361">yenileme dönemi</span><span class="sxs-lookup"><span data-stu-id="08845-361">renewal-period</span></span>|<span data-ttu-id="08845-362">Zaman aralığını saniye olarak geçmesi kota sıfırlar.</span><span class="sxs-lookup"><span data-stu-id="08845-362">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="08845-363">Evet</span><span class="sxs-lookup"><span data-stu-id="08845-363">Yes</span></span>|<span data-ttu-id="08845-364">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-364">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="08845-365">Kullanım</span><span class="sxs-lookup"><span data-stu-id="08845-365">Usage</span></span>  
 <span data-ttu-id="08845-366">Bu ilke aşağıdaki ilkesi kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="08845-366">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="08845-367">**İlke bölümleri:** gelen</span><span class="sxs-lookup"><span data-stu-id="08845-367">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="08845-368">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="08845-368">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="08845-369"><a name="ValidateJWT"></a>JWT doğrula</span><span class="sxs-lookup"><span data-stu-id="08845-369"><a name="ValidateJWT"></a> Validate JWT</span></span>  
 <span data-ttu-id="08845-370">`validate-jwt` İlkesi varlığı zorunlu kılan ve HTTP üstbilgisi veya belirtilen sorgu parametresi JWT geçerliliğini ya da belirtilen bir ayıklanır.</span><span class="sxs-lookup"><span data-stu-id="08845-370">The `validate-jwt` policy enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="08845-371">`validate-jwt` İlkesi gerektiriyor `exp` kayıtlı talep olan JWT belirteci inlcuded sürece `require-expiration-time` özniteliği belirtilen ve kümesine `false`.</span><span class="sxs-lookup"><span data-stu-id="08845-371">The `validate-jwt` policy requires that the `exp` registered claim is inlcuded in the JWT token, unless `require-expiration-time` attribute is specified and set to `false`.</span></span>  
> <span data-ttu-id="08845-372">`validate-jwt` İlkesi HS256 ve RS256 imza algoritmaları destekler.</span><span class="sxs-lookup"><span data-stu-id="08845-372">The `validate-jwt` policy supports HS256 and RS256 signing algorithms.</span></span> <span data-ttu-id="08845-373">HS256 için anahtar base64 ile kodlanmış form ilkesinde içi sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="08845-373">For HS256 the key must be provided inline within the policy in the base64 encoded form.</span></span> <span data-ttu-id="08845-374">RS256 için anahtar olmasını sağlamak bir Open ID yapılandırma uç noktası aracılığıyla sahiptir.</span><span class="sxs-lookup"><span data-stu-id="08845-374">For RS256 the key has to be provide via an Open ID configuration endpoint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="08845-375">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="08845-375">Policy statement</span></span>  
  
```xml  
<validate-jwt   
    header-name="name of http header containing the token (use query-parameter-name attribute if the token is passed in the URL)"   
    failed-validation-httpcode="http status code to return on failure"   
    failed-validation-error-message="error message to return on failure"   
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
    <claim name="name of the claim as it appears in the token" match="all|any">  
      <value>claim value as it is expected to appear in the token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of the configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="08845-376">Örnekler</span><span class="sxs-lookup"><span data-stu-id="08845-376">Examples</span></span>  
  
#### <a name="azure-mobile-services-token-validation"></a><span data-ttu-id="08845-377">Azure Mobile Services belirteci doğrulama</span><span class="sxs-lookup"><span data-stu-id="08845-377">Azure Mobile Services token validation</span></span>  
  
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
  
#### <a name="azure-active-directory-token-validation"></a><span data-ttu-id="08845-378">Azure Active Directory token doğrulama</span><span class="sxs-lookup"><span data-stu-id="08845-378">Azure Active Directory token validation</span></span>  
  
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

  
#### <a name="azure-active-directory-b2c-token-validation"></a><span data-ttu-id="08845-379">Azure Active Directory B2C belirteç doğrulama</span><span class="sxs-lookup"><span data-stu-id="08845-379">Azure Active Directory B2C token validation</span></span>  
  
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
  
#### <a name="authorize-access-to-operations-based-on-token-claims"></a><span data-ttu-id="08845-380">Belirteç talepleri temelinde işlemleri erişim yetkisi</span><span class="sxs-lookup"><span data-stu-id="08845-380">Authorize access to operations based on token claims</span></span>  
 <span data-ttu-id="08845-381">Bu örnek nasıl kullanılacağını gösterir [doğrulamak JWT](api-management-access-restriction-policies.md#ValidateJWT) işlemlerine erişim önceden yetkilendirmek için ilke tabanlı belirteç talep.</span><span class="sxs-lookup"><span data-stu-id="08845-381">This example shows how to use the [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) policy to pre-authorize access to operations based on token claims.</span></span> <span data-ttu-id="08845-382">Yapılandırma ve bu ilkeyi kullanan bir örnek için bkz: [bulut kapak bölüm 177: daha Vlad Vinogradsky ile yönetim özelliklerini API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) ve ileri sarma 13:50.</span><span class="sxs-lookup"><span data-stu-id="08845-382">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 13:50.</span></span> <span data-ttu-id="08845-383">İlke Düzenleyicisi'nde yapılandırılmış ilkeler görmek için 15:00 ve 18:50 hem ile hem de gerekli yetkilendirme belirteci olmadan Geliştirici portalından bir işlem arama tanıtımı için ileri sarma.</span><span class="sxs-lookup"><span data-stu-id="08845-383">Fast forward to 15:00 to see the policies configured in the policy editor and then to 18:50 for a demonstration of calling an operation from the developer portal both with and without the required authorization token.</span></span>  
  
```xml  
<!-- Copy the following snippet into the inbound section at the api (or higher) level to pre-authorize access to operations based on token claims -->  
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
  
### <a name="elements"></a><span data-ttu-id="08845-384">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="08845-384">Elements</span></span>  
  
|<span data-ttu-id="08845-385">Öğesi</span><span class="sxs-lookup"><span data-stu-id="08845-385">Element</span></span>|<span data-ttu-id="08845-386">Açıklama</span><span class="sxs-lookup"><span data-stu-id="08845-386">Description</span></span>|<span data-ttu-id="08845-387">Gerekli</span><span class="sxs-lookup"><span data-stu-id="08845-387">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="08845-388">doğrulama jwt</span><span class="sxs-lookup"><span data-stu-id="08845-388">validate-jwt</span></span>|<span data-ttu-id="08845-389">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="08845-389">Root element.</span></span>|<span data-ttu-id="08845-390">Evet</span><span class="sxs-lookup"><span data-stu-id="08845-390">Yes</span></span>|  
|<span data-ttu-id="08845-391">Hedef kitle</span><span class="sxs-lookup"><span data-stu-id="08845-391">audiences</span></span>|<span data-ttu-id="08845-392">Belirteçte mevcut olabilecek kabul edilebilir İzleyici talep listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="08845-392">Contains a list of acceptable audience claims that can be present on the token.</span></span> <span data-ttu-id="08845-393">Birden fazla hedef kitle değer mevcut sonra her değer denenir kadar tüm (Bu durumda doğrulama başarısız) tükendiği veya biri başarılı olana kadar.</span><span class="sxs-lookup"><span data-stu-id="08845-393">If multiple audience values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span> <span data-ttu-id="08845-394">En az bir hedef kitle belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="08845-394">At least one audience must be specified.</span></span>|<span data-ttu-id="08845-395">Hayır</span><span class="sxs-lookup"><span data-stu-id="08845-395">No</span></span>|  
|<span data-ttu-id="08845-396">verici İmzalama anahtarları</span><span class="sxs-lookup"><span data-stu-id="08845-396">issuer-signing-keys</span></span>|<span data-ttu-id="08845-397">İmzalanmış belirteçleri doğrulamak için kullanılan güvenlik Base64 ile kodlanmış anahtarları listesi.</span><span class="sxs-lookup"><span data-stu-id="08845-397">A list of Base64-encoded security keys used to validate signed tokens.</span></span> <span data-ttu-id="08845-398">Birden çok güvenlik anahtarları varsa sonra her anahtar denenir kadar tüm (Bu durumda doğrulama başarısız) tükendiği veya biri (belirteci geçiş işlemi için yararlıdır) başarılı olana kadar.</span><span class="sxs-lookup"><span data-stu-id="08845-398">If multiple security keys are present, then each key is tried until either all are exhausted (in which case validation fails) or until one succeeds (useful for token rollover).</span></span> <span data-ttu-id="08845-399">Anahtar öğeleri sahip isteğe bağlı bir `id` karşı eşleştirmek için kullanılan öznitelik `kid` talep.</span><span class="sxs-lookup"><span data-stu-id="08845-399">Key elements have an optional `id` attribute used to match against `kid` claim.</span></span>|<span data-ttu-id="08845-400">Hayır</span><span class="sxs-lookup"><span data-stu-id="08845-400">No</span></span>|  
|<span data-ttu-id="08845-401">verenler</span><span class="sxs-lookup"><span data-stu-id="08845-401">issuers</span></span>|<span data-ttu-id="08845-402">Belirtecin kabul edilebilir sorumluların listesini.</span><span class="sxs-lookup"><span data-stu-id="08845-402">A list of acceptable principals that issued the token.</span></span> <span data-ttu-id="08845-403">Birden çok veren değer mevcut sonra her değer denenir kadar tüm (Bu durumda doğrulama başarısız) tükendiği veya biri başarılı olana kadar.</span><span class="sxs-lookup"><span data-stu-id="08845-403">If multiple issuer values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span>|<span data-ttu-id="08845-404">Hayır</span><span class="sxs-lookup"><span data-stu-id="08845-404">No</span></span>|  
|<span data-ttu-id="08845-405">openıd-config</span><span class="sxs-lookup"><span data-stu-id="08845-405">openid-config</span></span>|<span data-ttu-id="08845-406">İçinden İmzalama anahtarları ve veren alınabilir uyumlu bir Open ID yapılandırma endpoint belirtmek için kullanılan öğe.</span><span class="sxs-lookup"><span data-stu-id="08845-406">The element used for specifying a compliant Open ID configuration endpoint from which signing keys and issuer can be obtained.</span></span>|<span data-ttu-id="08845-407">Hayır</span><span class="sxs-lookup"><span data-stu-id="08845-407">No</span></span>|  
|<span data-ttu-id="08845-408">gerekli talep</span><span class="sxs-lookup"><span data-stu-id="08845-408">required-claims</span></span>|<span data-ttu-id="08845-409">Talep belirteci için geçerli kabul edilebilmesi için mevcut olması beklenen listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="08845-409">Contains a list of claims expected to be present on the token for it to be considered valid.</span></span> <span data-ttu-id="08845-410">Zaman `match` özniteliği `all` her talep değeri ilkesinde başarılı olması doğrulama belirteci mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="08845-410">When the `match` attribute is set to `all` every claim value in the policy must be present in the token for validation to succeed.</span></span> <span data-ttu-id="08845-411">Zaman `match` özniteliği `any` en az bir talep belirteci başarılı olması doğrulama için mevcut olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="08845-411">When the `match` attribute is set to `any` at least one claim must be present in the token for validation to succeed.</span></span>|<span data-ttu-id="08845-412">Hayır</span><span class="sxs-lookup"><span data-stu-id="08845-412">No</span></span>|  
|<span data-ttu-id="08845-413">zumo ana anahtarı</span><span class="sxs-lookup"><span data-stu-id="08845-413">zumo-master-key</span></span>|<span data-ttu-id="08845-414">Ana anahtar için Azure Mobile Services tarafından yayınlanan belirteçleri</span><span class="sxs-lookup"><span data-stu-id="08845-414">Master key for tokens issued by Azure Mobile Services</span></span>|<span data-ttu-id="08845-415">Hayır</span><span class="sxs-lookup"><span data-stu-id="08845-415">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="08845-416">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="08845-416">Attributes</span></span>  
  
|<span data-ttu-id="08845-417">Ad</span><span class="sxs-lookup"><span data-stu-id="08845-417">Name</span></span>|<span data-ttu-id="08845-418">Açıklama</span><span class="sxs-lookup"><span data-stu-id="08845-418">Description</span></span>|<span data-ttu-id="08845-419">Gerekli</span><span class="sxs-lookup"><span data-stu-id="08845-419">Required</span></span>|<span data-ttu-id="08845-420">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="08845-420">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="08845-421">saat eğriltme</span><span class="sxs-lookup"><span data-stu-id="08845-421">clock-skew</span></span>|<span data-ttu-id="08845-422">TimeSpan.</span><span class="sxs-lookup"><span data-stu-id="08845-422">Timespan.</span></span> <span data-ttu-id="08845-423">Belirtecin sona erme talep belirteçte ve geçerli tarihi durumda bazı küçük leeway sağlar / saat.</span><span class="sxs-lookup"><span data-stu-id="08845-423">Provides some small leeway in case the token's expiration claim is present in the token and is past the current date / time.</span></span>|<span data-ttu-id="08845-424">Hayır</span><span class="sxs-lookup"><span data-stu-id="08845-424">No</span></span>|<span data-ttu-id="08845-425">0 saniye</span><span class="sxs-lookup"><span data-stu-id="08845-425">0 seconds</span></span>|  
|<span data-ttu-id="08845-426">başarısız oldu-doğrulama-hata iletisi</span><span class="sxs-lookup"><span data-stu-id="08845-426">failed-validation-error-message</span></span>|<span data-ttu-id="08845-427">JWT doğrulamayı geçemezse HTTP yanıt gövdesinde döndürmek için hata iletisi.</span><span class="sxs-lookup"><span data-stu-id="08845-427">Error message to return in the HTTP response body if the JWT does not pass validation.</span></span> <span data-ttu-id="08845-428">Bu ileti, tüm özel karakterleri düzgün şekilde çıkıldığından olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="08845-428">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="08845-429">Hayır</span><span class="sxs-lookup"><span data-stu-id="08845-429">No</span></span>|<span data-ttu-id="08845-430">Varsayılan hata iletisini doğrulama sorunu, örneğin "JWT mevcut değil." bağlıdır</span><span class="sxs-lookup"><span data-stu-id="08845-430">Default error message depends on validation issue, for example "JWT not present."</span></span>|  
|<span data-ttu-id="08845-431">başarısız oldu-doğrulama-httpcode</span><span class="sxs-lookup"><span data-stu-id="08845-431">failed-validation-httpcode</span></span>|<span data-ttu-id="08845-432">JWT doğrulama geçmiyor ise döndürülecek HTTP durum kodu.</span><span class="sxs-lookup"><span data-stu-id="08845-432">HTTP Status code to return if the JWT doesn't pass validation.</span></span>|<span data-ttu-id="08845-433">Hayır</span><span class="sxs-lookup"><span data-stu-id="08845-433">No</span></span>|<span data-ttu-id="08845-434">401</span><span class="sxs-lookup"><span data-stu-id="08845-434">401</span></span>|  
|<span data-ttu-id="08845-435">üstbilgi adı</span><span class="sxs-lookup"><span data-stu-id="08845-435">header-name</span></span>|<span data-ttu-id="08845-436">Belirteç bulunduran HTTP üstbilgisinin adı.</span><span class="sxs-lookup"><span data-stu-id="08845-436">The name of the HTTP header holding the token.</span></span>|<span data-ttu-id="08845-437">Ya da `header-name` veya `query-paremeter-name` belirtilmelidir; ancak ikisi birden değil.</span><span class="sxs-lookup"><span data-stu-id="08845-437">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="08845-438">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-438">N/A</span></span>|  
|<span data-ttu-id="08845-439">id</span><span class="sxs-lookup"><span data-stu-id="08845-439">id</span></span>|<span data-ttu-id="08845-440">`id` Özniteliği `key` öğesi karşı eşleşen dize belirtmenize olanak verir `kid` imza doğrulama için kullanılacak uygun anahtarını bulmak (varsa) belirteç talep.</span><span class="sxs-lookup"><span data-stu-id="08845-440">The `id` attribute on the `key` element allows you to specify the string that will be matched against `kid` claim in the token (if present) to find out the appropriate key to use for signature validation.</span></span>|<span data-ttu-id="08845-441">Hayır</span><span class="sxs-lookup"><span data-stu-id="08845-441">No</span></span>|<span data-ttu-id="08845-442">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-442">N/A</span></span>|  
|<span data-ttu-id="08845-443">eşleşme</span><span class="sxs-lookup"><span data-stu-id="08845-443">match</span></span>|<span data-ttu-id="08845-444">`match` Özniteliği `claim` öğesi ilkedeki her talep değeri başarılı olması doğrulama belirteçte mevcut olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="08845-444">The `match` attribute on the `claim` element specifies whether every claim value in the policy must be present in the token for validation to succeed.</span></span> <span data-ttu-id="08845-445">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="08845-445">Possible values are:</span></span><br /><br /> <span data-ttu-id="08845-446">-                          `all`-her talep değeri ilkesinde başarılı olması doğrulama belirteci mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="08845-446">-                          `all` - every claim value in the policy must be present in the token for validation to succeed.</span></span><br /><br /> <span data-ttu-id="08845-447">-                          `any`-en az bir talep değeri başarılı olması doğrulama belirteci mevcut olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="08845-447">-                          `any` - at least one claim value must be present in the token for validation to succeed.</span></span>|<span data-ttu-id="08845-448">Hayır</span><span class="sxs-lookup"><span data-stu-id="08845-448">No</span></span>|<span data-ttu-id="08845-449">Tüm</span><span class="sxs-lookup"><span data-stu-id="08845-449">all</span></span>|  
|<span data-ttu-id="08845-450">Sorgu paremeter adı</span><span class="sxs-lookup"><span data-stu-id="08845-450">query-paremeter-name</span></span>|<span data-ttu-id="08845-451">Adını belirteci bulunduran sorgu parametresi.</span><span class="sxs-lookup"><span data-stu-id="08845-451">The name of the the query parameter holding the token.</span></span>|<span data-ttu-id="08845-452">Ya da `header-name` veya `query-paremeter-name` belirtilmelidir; ancak ikisi birden değil.</span><span class="sxs-lookup"><span data-stu-id="08845-452">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="08845-453">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-453">N/A</span></span>|  
|<span data-ttu-id="08845-454">gerekli-sona erme-time</span><span class="sxs-lookup"><span data-stu-id="08845-454">require-expiration-time</span></span>|<span data-ttu-id="08845-455">Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="08845-455">Boolean.</span></span> <span data-ttu-id="08845-456">Bir süre sonu talep belirteçte gerekip gerekmediğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="08845-456">Specifies whether an expiration claim is required in the token.</span></span>|<span data-ttu-id="08845-457">Hayır</span><span class="sxs-lookup"><span data-stu-id="08845-457">No</span></span>|<span data-ttu-id="08845-458">TRUE</span><span class="sxs-lookup"><span data-stu-id="08845-458">true</span></span>|
|<span data-ttu-id="08845-459">gerektiren düzeni</span><span class="sxs-lookup"><span data-stu-id="08845-459">require-scheme</span></span>|<span data-ttu-id="08845-460">Belirteç adını düzen, örn. "Bearer".</span><span class="sxs-lookup"><span data-stu-id="08845-460">The name of the token scheme, e.g. "Bearer".</span></span> <span data-ttu-id="08845-461">Bu öznitelik ayarlandığında, ilke yetkilendirme üst bilgisi değeri, belirtilen düzeni bulunduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="08845-461">When this attribute is set, the policy will ensure that specified scheme is present in the Authorization header value.</span></span>|<span data-ttu-id="08845-462">Hayır</span><span class="sxs-lookup"><span data-stu-id="08845-462">No</span></span>|<span data-ttu-id="08845-463">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-463">N/A</span></span>|
|<span data-ttu-id="08845-464">gerekli-oturum-belirteçleri</span><span class="sxs-lookup"><span data-stu-id="08845-464">require-signed-tokens</span></span>|<span data-ttu-id="08845-465">Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="08845-465">Boolean.</span></span> <span data-ttu-id="08845-466">Bir belirteç imzalanmasını gerekli olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="08845-466">Specifies whether a token is required to be signed.</span></span>|<span data-ttu-id="08845-467">Hayır</span><span class="sxs-lookup"><span data-stu-id="08845-467">No</span></span>|<span data-ttu-id="08845-468">TRUE</span><span class="sxs-lookup"><span data-stu-id="08845-468">true</span></span>|  
|<span data-ttu-id="08845-469">URL</span><span class="sxs-lookup"><span data-stu-id="08845-469">url</span></span>|<span data-ttu-id="08845-470">Burada Open ID yapılandırma meta verilerini elde edilebilir gelen kimliği yapılandırma uç noktasının URL'sini açın.</span><span class="sxs-lookup"><span data-stu-id="08845-470">Open ID configuration endpoint URL from where Open ID configuration metadata can be obtained.</span></span> <span data-ttu-id="08845-471">Azure Active Directory için şu URL'yi kullanın: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` directory Kiracı adınız, örneğin değiştirerek `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="08845-471">For Azure Active Directory use the following URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` substituting your directory tenant name, e.g. `contoso.onmicrosoft.com`.</span></span>|<span data-ttu-id="08845-472">Evet</span><span class="sxs-lookup"><span data-stu-id="08845-472">Yes</span></span>|<span data-ttu-id="08845-473">Yok</span><span class="sxs-lookup"><span data-stu-id="08845-473">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="08845-474">Kullanım</span><span class="sxs-lookup"><span data-stu-id="08845-474">Usage</span></span>  
 <span data-ttu-id="08845-475">Bu ilke aşağıdaki ilkesi kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="08845-475">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="08845-476">**İlke bölümleri:** gelen</span><span class="sxs-lookup"><span data-stu-id="08845-476">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="08845-477">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="08845-477">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="08845-478">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="08845-478">Next steps</span></span>
<span data-ttu-id="08845-479">İlkeleriyle çalışma daha fazla bilgi için bkz: [API Management ilkeleri](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="08845-479">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
