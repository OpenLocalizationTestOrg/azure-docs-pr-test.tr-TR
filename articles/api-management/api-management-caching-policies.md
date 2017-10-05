---
title: "Azure API Management önbelleğe alma ilkeleri | Microsoft Docs"
description: "Azure API Management'te kullanıma önbelleğe alma ilkeleri hakkında bilgi edinin."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 8147199c-24d8-439f-b2a9-da28a70a890c
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2a8f012e7e223ef5c1683c8a6c5ecf2f3e96bed8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-caching-policies"></a><span data-ttu-id="bcd58-103">API Management önbelleğe alma ilkeleri</span><span class="sxs-lookup"><span data-stu-id="bcd58-103">API Management caching policies</span></span>
<span data-ttu-id="bcd58-104">Bu konu aşağıdaki API Management ilkeleri bir başvuru sağlar.</span><span class="sxs-lookup"><span data-stu-id="bcd58-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="bcd58-105">Ekleme ve ilkeleri yapılandırma hakkında daha fazla bilgi için bkz: [API Management ilkeleri](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="bcd58-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="bcd58-106"><a name="CachingPolicies"></a>Önbelleğe alma ilkeleri</span><span class="sxs-lookup"><span data-stu-id="bcd58-106"><a name="CachingPolicies"></a> Caching policies</span></span>  
  
-   <span data-ttu-id="bcd58-107">Yanıt önbelleğe alma ilkeleri</span><span class="sxs-lookup"><span data-stu-id="bcd58-107">Response caching policies</span></span>  
  
    -   <span data-ttu-id="bcd58-108">[Önbellekten alma](api-management-caching-policies.md#GetFromCache) -önbellek gerçekleştirmek aramak ve geçerli bir önbelleğe alınan yanıtları kullanılabilir olduğunda döndürür.</span><span class="sxs-lookup"><span data-stu-id="bcd58-108">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached responses when available.</span></span>  
  
    -   <span data-ttu-id="bcd58-109">[Önbellek deposuna](api-management-caching-policies.md#StoreToCache) -belirtilen önbellek denetim yapılandırmasında göre yanıtlarını önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="bcd58-109">[Store to cache](api-management-caching-policies.md#StoreToCache) - Caches responses according to the specified cache control configuration.</span></span>  
  
-   <span data-ttu-id="bcd58-110">Değer önbelleğe alma ilkeleri</span><span class="sxs-lookup"><span data-stu-id="bcd58-110">Value caching policies</span></span>  
  
    -   <span data-ttu-id="bcd58-111">[Önbelleğe alınan değer alma](#GetFromCacheByKey) -anahtar tarafından önbelleğe alınmış bir öğeyi geri almak.</span><span class="sxs-lookup"><span data-stu-id="bcd58-111">[Get value from cache](#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="bcd58-112">[Değer önbellekte depolamak](#StoreToCacheByKey) -bir öğe anahtarı tarafından önbellekte depolamak.</span><span class="sxs-lookup"><span data-stu-id="bcd58-112">[Store value in cache](#StoreToCacheByKey) - Store an item in the cache by key.</span></span>  
  
    -   <span data-ttu-id="bcd58-113">[Önbelleğe alınan değer kaldırmak](#RemoveCacheByKey) -öğenin önbellekte anahtarının kaldırın.</span><span class="sxs-lookup"><span data-stu-id="bcd58-113">[Remove value from cache](#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>  
  
##  <span data-ttu-id="bcd58-114"><a name="GetFromCache"></a>Önbellekten alma</span><span class="sxs-lookup"><span data-stu-id="bcd58-114"><a name="GetFromCache"></a> Get from cache</span></span>  
 <span data-ttu-id="bcd58-115">Kullanım `cache-lookup` önbellek gerçekleştirilecek İlkesi aramak ve geçerli bir önbelleğe alınan yanıt kullanılabilir olduğunda döndürür.</span><span class="sxs-lookup"><span data-stu-id="bcd58-115">Use the `cache-lookup` policy to perform cache look up and return a valid cached response when available.</span></span> <span data-ttu-id="bcd58-116">Bu ilke, yanıt içeriği bir süre boyunca statik kalır olduğu durumlarda uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="bcd58-116">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="bcd58-117">Yanıt önbelleğe alma bant genişliğini azaltır ve işleme gereksinimlerini gecikmede API tüketiciler tarafından algılanan arka uç web sunucusu ve düşürmeye uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="bcd58-117">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="bcd58-118">Bu ilke karşılık gelen olmalıdır [önbellek deposuna](api-management-caching-policies.md#StoreToCache) ilkesi.</span><span class="sxs-lookup"><span data-stu-id="bcd58-118">This policy must have a corresponding [Store to cache](api-management-caching-policies.md#StoreToCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bcd58-119">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="bcd58-119">Policy statement</span></span>  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression to evaluate)">  
  <vary-by-header>Accept</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Accept-Charset</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Authorization</vary-by-header>  
  <!-- should be present when allow-authorized-response-caching is "true"-->  
  <vary-by-header>header name</vary-by-header>  
  <!-- optional, can repeated several times -->  
  <vary-by-query-parameter>parameter name</vary-by-query-parameter>  
  <!-- optional, can repeated several times -->  
</cache-lookup>  
```  
  
### <a name="examples"></a><span data-ttu-id="bcd58-120">Örnekler</span><span class="sxs-lookup"><span data-stu-id="bcd58-120">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="bcd58-121">Örnek</span><span class="sxs-lookup"><span data-stu-id="bcd58-121">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="none" must-revalidate="true">  
            <vary-by-query-parameter>version</vary-by-query-parameter>  
        </cache-lookup>           
    </inbound>  
    <outbound>  
        <cache-store duration="seconds" />  
        <base />          
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="bcd58-122">Örnek ilke ifadeleri kullanma</span><span class="sxs-lookup"><span data-stu-id="bcd58-122">Example using policy expressions</span></span>  
 <span data-ttu-id="bcd58-123">Bu örnek nasıl API Management yanıt önbelleğe alma yanıt arka uç hizmeti olarak önbelleğe almayı eşleşen süresi yapılandırmak için yedeklenmiş hizmetin tarafından belirtilen gösterir `Cache-Control` yönergesi.</span><span class="sxs-lookup"><span data-stu-id="bcd58-123">This example shows how to to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="bcd58-124">Yapılandırma ve bu ilkeyi kullanan bir örnek için bkz: [bulut kapak bölüm 177: daha Vlad Vinogradsky ile yönetim özelliklerini API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) ve 25:25 için ileri sarma.</span><span class="sxs-lookup"><span data-stu-id="bcd58-124">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span></span>  
  
```xml  
<!-- The following cache policy snippets demonstrate how to control API Management reponse cache duration with Cache-Control headers sent by the backend service. -->  
  
<!-- Copy this snippet into the inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into the outbound section. Note that cache duration is set to the max-age value provided in the Cache-Control header received from the backend service or to the deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="bcd58-125">Daha fazla bilgi için bkz: [ilke ifadelerini](api-management-policy-expressions.md) ve [bağlamının](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="bcd58-125">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="bcd58-126">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="bcd58-126">Elements</span></span>  
  
|<span data-ttu-id="bcd58-127">Ad</span><span class="sxs-lookup"><span data-stu-id="bcd58-127">Name</span></span>|<span data-ttu-id="bcd58-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bcd58-128">Description</span></span>|<span data-ttu-id="bcd58-129">Gerekli</span><span class="sxs-lookup"><span data-stu-id="bcd58-129">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="bcd58-130">Önbellek araması</span><span class="sxs-lookup"><span data-stu-id="bcd58-130">cache-lookup</span></span>|<span data-ttu-id="bcd58-131">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="bcd58-131">Root element.</span></span>|<span data-ttu-id="bcd58-132">Evet</span><span class="sxs-lookup"><span data-stu-id="bcd58-132">Yes</span></span>|  
|<span data-ttu-id="bcd58-133">farklılık tarafından-üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="bcd58-133">vary-by-header</span></span>|<span data-ttu-id="bcd58-134">Ana bilgisayardan kabul, Accept-Charset, Accept-Encoding, Accept-Language, yetkilendirme gibi Expect, belirtilen üstbilgi değerini başına yanıtlarını önbelleğe alma Başlat IF-Match.</span><span class="sxs-lookup"><span data-stu-id="bcd58-134">Start caching responses per value of specified header, such as Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span></span>|<span data-ttu-id="bcd58-135">Hayır</span><span class="sxs-lookup"><span data-stu-id="bcd58-135">No</span></span>|  
|<span data-ttu-id="bcd58-136">farklılık-tarafından-query-parametresi</span><span class="sxs-lookup"><span data-stu-id="bcd58-136">vary-by-query-parameter</span></span>|<span data-ttu-id="bcd58-137">Her değeri belirtilen sorgu parametrelerinin yanıtlarını önbelleğe alma başlatın.</span><span class="sxs-lookup"><span data-stu-id="bcd58-137">Start caching responses per value of specified query parameters.</span></span> <span data-ttu-id="bcd58-138">Tek bir veya birden çok parametre girin.</span><span class="sxs-lookup"><span data-stu-id="bcd58-138">Enter a single or multiple parameters.</span></span> <span data-ttu-id="bcd58-139">Ayırıcı olarak virgül kullanın.</span><span class="sxs-lookup"><span data-stu-id="bcd58-139">Use semicolon as a separator.</span></span> <span data-ttu-id="bcd58-140">Hiçbiri belirtilmezse, tüm sorgu parametreleri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bcd58-140">If none are specified, all query parameters are used.</span></span>|<span data-ttu-id="bcd58-141">Hayır</span><span class="sxs-lookup"><span data-stu-id="bcd58-141">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bcd58-142">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="bcd58-142">Attributes</span></span>  
  
|<span data-ttu-id="bcd58-143">Ad</span><span class="sxs-lookup"><span data-stu-id="bcd58-143">Name</span></span>|<span data-ttu-id="bcd58-144">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bcd58-144">Description</span></span>|<span data-ttu-id="bcd58-145">Gerekli</span><span class="sxs-lookup"><span data-stu-id="bcd58-145">Required</span></span>|<span data-ttu-id="bcd58-146">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="bcd58-146">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="bcd58-147">izin ver-özel-yanıt-önbelleğe alma</span><span class="sxs-lookup"><span data-stu-id="bcd58-147">allow-private-response-caching</span></span>|<span data-ttu-id="bcd58-148">Ayarlandığında `true`, bir Authorization üstbilgisi içeren istekleri önbelleğe alma sağlar.</span><span class="sxs-lookup"><span data-stu-id="bcd58-148">When set to `true`, allows caching of requests that contain an Authorization header.</span></span>|<span data-ttu-id="bcd58-149">Hayır</span><span class="sxs-lookup"><span data-stu-id="bcd58-149">No</span></span>|<span data-ttu-id="bcd58-150">False</span><span class="sxs-lookup"><span data-stu-id="bcd58-150">false</span></span>|  
|<span data-ttu-id="bcd58-151">önbelleğe alma aşağı akış türü</span><span class="sxs-lookup"><span data-stu-id="bcd58-151">downstream-caching-type</span></span>|<span data-ttu-id="bcd58-152">Bu öznitelik aşağıdaki değerlerden birine ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bcd58-152">This attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="bcd58-153">-none - aşağı akış önbelleğe alma izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="bcd58-153">-   none - downstream caching is not allowed.</span></span><br /><span data-ttu-id="bcd58-154">-Özel - aşağı akış özel önbelleğe alma izin verilir.</span><span class="sxs-lookup"><span data-stu-id="bcd58-154">-   private - downstream private caching is allowed.</span></span><br /><span data-ttu-id="bcd58-155">-Genel - özel ve paylaşılan aşağı akış önbelleğe alma izin verilir.</span><span class="sxs-lookup"><span data-stu-id="bcd58-155">-   public - private and shared downstream caching is allowed.</span></span>|<span data-ttu-id="bcd58-156">Hayır</span><span class="sxs-lookup"><span data-stu-id="bcd58-156">No</span></span>|<span data-ttu-id="bcd58-157">Yok</span><span class="sxs-lookup"><span data-stu-id="bcd58-157">none</span></span>|  
|<span data-ttu-id="bcd58-158">gereken revalidate</span><span class="sxs-lookup"><span data-stu-id="bcd58-158">must-revalidate</span></span>|<span data-ttu-id="bcd58-159">Aşağı Akış önbelleği etkin olduğunda, bu öznitelik açar veya kapatır `must-revalidate` ağ geçidi yanıtlarındaki önbellek denetimi yönergesi.</span><span class="sxs-lookup"><span data-stu-id="bcd58-159">When downstream caching is enabled this attribute turns on or off  the `must-revalidate` cache control directive in gateway responses.</span></span>|<span data-ttu-id="bcd58-160">Hayır</span><span class="sxs-lookup"><span data-stu-id="bcd58-160">No</span></span>|<span data-ttu-id="bcd58-161">TRUE</span><span class="sxs-lookup"><span data-stu-id="bcd58-161">true</span></span>|  
|<span data-ttu-id="bcd58-162">farklılık-tarafından-Geliştirici</span><span class="sxs-lookup"><span data-stu-id="bcd58-162">vary-by-developer</span></span>|<span data-ttu-id="bcd58-163">Kümesine `true` Geliştirici anahtar başına önbellek yanıtları.</span><span class="sxs-lookup"><span data-stu-id="bcd58-163">Set to `true` to cache responses per developer key.</span></span>|<span data-ttu-id="bcd58-164">Hayır</span><span class="sxs-lookup"><span data-stu-id="bcd58-164">No</span></span>|<span data-ttu-id="bcd58-165">False</span><span class="sxs-lookup"><span data-stu-id="bcd58-165">false</span></span>|  
|<span data-ttu-id="bcd58-166">farklılık tarafından-Geliştirici-grupları</span><span class="sxs-lookup"><span data-stu-id="bcd58-166">vary-by-developer-groups</span></span>|<span data-ttu-id="bcd58-167">Kümesine `true` kullanıcı rol başına önbellek yanıtları.</span><span class="sxs-lookup"><span data-stu-id="bcd58-167">Set to `true` to cache responses per user role.</span></span>|<span data-ttu-id="bcd58-168">Hayır</span><span class="sxs-lookup"><span data-stu-id="bcd58-168">No</span></span>|<span data-ttu-id="bcd58-169">False</span><span class="sxs-lookup"><span data-stu-id="bcd58-169">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bcd58-170">Kullanım</span><span class="sxs-lookup"><span data-stu-id="bcd58-170">Usage</span></span>  
 <span data-ttu-id="bcd58-171">Bu ilke aşağıdaki ilkesi kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bcd58-171">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bcd58-172">**İlke bölümleri:** gelen</span><span class="sxs-lookup"><span data-stu-id="bcd58-172">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="bcd58-173">**İlke kapsamları:** API işlemi, ürün</span><span class="sxs-lookup"><span data-stu-id="bcd58-173">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="bcd58-174"><a name="StoreToCache"></a>Önbelleğine depolamak</span><span class="sxs-lookup"><span data-stu-id="bcd58-174"><a name="StoreToCache"></a> Store to cache</span></span>  
 <span data-ttu-id="bcd58-175">`cache-store` İlkesi belirtilen önbellek ayarlara göre yanıtlarını önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="bcd58-175">The `cache-store` policy caches responses according to the specified cache settings.</span></span> <span data-ttu-id="bcd58-176">Bu ilke, yanıt içeriği bir süre boyunca statik kalır olduğu durumlarda uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="bcd58-176">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="bcd58-177">Yanıt önbelleğe alma bant genişliğini azaltır ve işleme gereksinimlerini gecikmede API tüketiciler tarafından algılanan arka uç web sunucusu ve düşürmeye uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="bcd58-177">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="bcd58-178">Bu ilke karşılık gelen olmalıdır [önbellekten alma](api-management-caching-policies.md#GetFromCache) ilkesi.</span><span class="sxs-lookup"><span data-stu-id="bcd58-178">This policy must have a corresponding [Get from cache](api-management-caching-policies.md#GetFromCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bcd58-179">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="bcd58-179">Policy statement</span></span>  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a><span data-ttu-id="bcd58-180">Örnekler</span><span class="sxs-lookup"><span data-stu-id="bcd58-180">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="bcd58-181">Örnek</span><span class="sxs-lookup"><span data-stu-id="bcd58-181">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
          <cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false">  
                <vary-by-query-parameter>parameter name</vary-by-query-parameter> <!-- optional, can repeated several times -->  
        </cache-lookup>  
    </inbound>  
    <outbound>  
        <base />  
            <cache-store duration="3600" />  
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="bcd58-182">Örnek ilke ifadeleri kullanma</span><span class="sxs-lookup"><span data-stu-id="bcd58-182">Example using policy expressions</span></span>  
 <span data-ttu-id="bcd58-183">Bu örnek nasıl API Management yanıt önbelleğe alma yanıt arka uç hizmeti olarak önbelleğe almayı eşleşen süresi yapılandırmak için yedeklenmiş hizmetin tarafından belirtilen gösterir `Cache-Control` yönergesi.</span><span class="sxs-lookup"><span data-stu-id="bcd58-183">This example shows how to to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="bcd58-184">Yapılandırma ve bu ilkeyi kullanan bir örnek için bkz: [bulut kapak bölüm 177: daha Vlad Vinogradsky ile yönetim özelliklerini API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) ve 25:25 için ileri sarma.</span><span class="sxs-lookup"><span data-stu-id="bcd58-184">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span></span>  
  
```xml  
<!-- The following cache policy snippets demonstrate how to control API Management reponse cache duration with Cache-Control headers sent by the backend service. -->  
  
<!-- Copy this snippet into the inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into the outbound section. Note that cache duration is set to the max-age value provided in the Cache-Control header received from the backend service or to the deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="bcd58-185">Daha fazla bilgi için bkz: [ilke ifadelerini](api-management-policy-expressions.md) ve [bağlamının](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="bcd58-185">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="bcd58-186">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="bcd58-186">Elements</span></span>  
  
|<span data-ttu-id="bcd58-187">Ad</span><span class="sxs-lookup"><span data-stu-id="bcd58-187">Name</span></span>|<span data-ttu-id="bcd58-188">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bcd58-188">Description</span></span>|<span data-ttu-id="bcd58-189">Gerekli</span><span class="sxs-lookup"><span data-stu-id="bcd58-189">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="bcd58-190">Önbellek deposu</span><span class="sxs-lookup"><span data-stu-id="bcd58-190">cache-store</span></span>|<span data-ttu-id="bcd58-191">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="bcd58-191">Root element.</span></span>|<span data-ttu-id="bcd58-192">Evet</span><span class="sxs-lookup"><span data-stu-id="bcd58-192">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bcd58-193">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="bcd58-193">Attributes</span></span>  
  
|<span data-ttu-id="bcd58-194">Ad</span><span class="sxs-lookup"><span data-stu-id="bcd58-194">Name</span></span>|<span data-ttu-id="bcd58-195">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bcd58-195">Description</span></span>|<span data-ttu-id="bcd58-196">Gerekli</span><span class="sxs-lookup"><span data-stu-id="bcd58-196">Required</span></span>|<span data-ttu-id="bcd58-197">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="bcd58-197">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="bcd58-198">Süre</span><span class="sxs-lookup"><span data-stu-id="bcd58-198">duration</span></span>|<span data-ttu-id="bcd58-199">Zaman yaşam saniye cinsinden belirtilen önbelleğe alınmış girişlerinin.</span><span class="sxs-lookup"><span data-stu-id="bcd58-199">Time-to-live of the cached entries, specified in seconds.</span></span>|<span data-ttu-id="bcd58-200">Evet</span><span class="sxs-lookup"><span data-stu-id="bcd58-200">Yes</span></span>|<span data-ttu-id="bcd58-201">Yok</span><span class="sxs-lookup"><span data-stu-id="bcd58-201">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bcd58-202">Kullanım</span><span class="sxs-lookup"><span data-stu-id="bcd58-202">Usage</span></span>  
 <span data-ttu-id="bcd58-203">Bu ilke aşağıdaki ilkesi kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bcd58-203">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bcd58-204">**İlke bölümleri:** giden</span><span class="sxs-lookup"><span data-stu-id="bcd58-204">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="bcd58-205">**İlke kapsamları:** API işlemi, ürün</span><span class="sxs-lookup"><span data-stu-id="bcd58-205">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="bcd58-206"><a name="GetFromCacheByKey"></a>Önbelleğe alınan değer alma</span><span class="sxs-lookup"><span data-stu-id="bcd58-206"><a name="GetFromCacheByKey"></a> Get value from cache</span></span>  
 <span data-ttu-id="bcd58-207">Kullanım `cache-lookup-value` İlkesi anahtarının önbellek araması gerçekleştirmek ve bir önbelleğe alınan değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="bcd58-207">Use the `cache-lookup-value` policy to perform cache lookup by key and return a cached value.</span></span> <span data-ttu-id="bcd58-208">Anahtar isteğe bağlı bir dize değerine sahip olabilir ve genellikle bir ilke ifade kullanılarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="bcd58-208">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="bcd58-209">Bu ilke karşılık gelen olmalıdır [değeri önbellekte depolamak](#StoreToCacheByKey) ilkesi.</span><span class="sxs-lookup"><span data-stu-id="bcd58-209">This policy must have a corresponding [Store value in cache](#StoreToCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bcd58-210">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="bcd58-210">Policy statement</span></span>  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value to use if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a><span data-ttu-id="bcd58-211">Örnek</span><span class="sxs-lookup"><span data-stu-id="bcd58-211">Example</span></span>  
 <span data-ttu-id="bcd58-212">Daha fazla bilgi ve bu ilkeyi örnekleri için bkz: [özel Azure API Management'te önbelleğe alma](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="bcd58-212">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="bcd58-213">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="bcd58-213">Elements</span></span>  
  
|<span data-ttu-id="bcd58-214">Ad</span><span class="sxs-lookup"><span data-stu-id="bcd58-214">Name</span></span>|<span data-ttu-id="bcd58-215">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bcd58-215">Description</span></span>|<span data-ttu-id="bcd58-216">Gerekli</span><span class="sxs-lookup"><span data-stu-id="bcd58-216">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="bcd58-217">Önbellek arama değeri</span><span class="sxs-lookup"><span data-stu-id="bcd58-217">cache-lookup-value</span></span>|<span data-ttu-id="bcd58-218">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="bcd58-218">Root element.</span></span>|<span data-ttu-id="bcd58-219">Evet</span><span class="sxs-lookup"><span data-stu-id="bcd58-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bcd58-220">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="bcd58-220">Attributes</span></span>  
  
|<span data-ttu-id="bcd58-221">Ad</span><span class="sxs-lookup"><span data-stu-id="bcd58-221">Name</span></span>|<span data-ttu-id="bcd58-222">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bcd58-222">Description</span></span>|<span data-ttu-id="bcd58-223">Gerekli</span><span class="sxs-lookup"><span data-stu-id="bcd58-223">Required</span></span>|<span data-ttu-id="bcd58-224">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="bcd58-224">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="bcd58-225">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="bcd58-225">default-value</span></span>|<span data-ttu-id="bcd58-226">Önbellek anahtar arama değişken IF atanacak bir değer bir isabetsizliği sonuçlandı.</span><span class="sxs-lookup"><span data-stu-id="bcd58-226">A value that will be assigned to the variable if the cache key lookup resulted in a miss.</span></span> <span data-ttu-id="bcd58-227">Bu özniteliği belirtilmezse, `null` atanır.</span><span class="sxs-lookup"><span data-stu-id="bcd58-227">If this attribute is not specified, `null` is assigned.</span></span>|<span data-ttu-id="bcd58-228">Hayır</span><span class="sxs-lookup"><span data-stu-id="bcd58-228">No</span></span>|`null`|  
|<span data-ttu-id="bcd58-229">anahtar</span><span class="sxs-lookup"><span data-stu-id="bcd58-229">key</span></span>|<span data-ttu-id="bcd58-230">Aramada kullanmak için önbellek anahtar değeri.</span><span class="sxs-lookup"><span data-stu-id="bcd58-230">Cache key value to use in the lookup.</span></span>|<span data-ttu-id="bcd58-231">Evet</span><span class="sxs-lookup"><span data-stu-id="bcd58-231">Yes</span></span>|<span data-ttu-id="bcd58-232">Yok</span><span class="sxs-lookup"><span data-stu-id="bcd58-232">N/A</span></span>|  
|<span data-ttu-id="bcd58-233">değişken adı</span><span class="sxs-lookup"><span data-stu-id="bcd58-233">variable-name</span></span>|<span data-ttu-id="bcd58-234">Adını [bağlamının](api-management-policy-expressions.md#ContextVariables) için arama başarılı ise yukarı looked değeri atanır.</span><span class="sxs-lookup"><span data-stu-id="bcd58-234">Name of the [context variable](api-management-policy-expressions.md#ContextVariables) the looked up value will be assigned to, if lookup is successful.</span></span> <span data-ttu-id="bcd58-235">Bir isabetsizliği arama sonuçları, değişkenin değeri atanacak `default-value` özniteliği veya `null`, `default-value` özniteliği atlanmış.</span><span class="sxs-lookup"><span data-stu-id="bcd58-235">If lookup results in a miss, the variable will be assigned the value of the `default-value` attribute or `null`, if the `default-value` attribute is omitted.</span></span>|<span data-ttu-id="bcd58-236">Evet</span><span class="sxs-lookup"><span data-stu-id="bcd58-236">Yes</span></span>|<span data-ttu-id="bcd58-237">Yok</span><span class="sxs-lookup"><span data-stu-id="bcd58-237">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bcd58-238">Kullanım</span><span class="sxs-lookup"><span data-stu-id="bcd58-238">Usage</span></span>  
 <span data-ttu-id="bcd58-239">Bu ilke aşağıdaki ilkesi kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bcd58-239">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bcd58-240">**İlke bölümleri:** gelen, giden arka uç, hata</span><span class="sxs-lookup"><span data-stu-id="bcd58-240">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bcd58-241">**İlke kapsamları:** Genel API, işlemi, ürünü</span><span class="sxs-lookup"><span data-stu-id="bcd58-241">**Policy scopes:** global, API, operation, product</span></span>  
  
##  <span data-ttu-id="bcd58-242"><a name="StoreToCacheByKey"></a>Önbellek deposu değeri</span><span class="sxs-lookup"><span data-stu-id="bcd58-242"><a name="StoreToCacheByKey"></a> Store value in cache</span></span>  
 <span data-ttu-id="bcd58-243">`cache-store-value` Önbellek depolama anahtarının gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="bcd58-243">The `cache-store-value` performs cache storage by key.</span></span> <span data-ttu-id="bcd58-244">Anahtar isteğe bağlı bir dize değerine sahip olabilir ve genellikle bir ilke ifade kullanılarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="bcd58-244">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="bcd58-245">Bu ilke karşılık gelen olmalıdır [değeri önbellekten alma](#GetFromCacheByKey) ilkesi.</span><span class="sxs-lookup"><span data-stu-id="bcd58-245">This policy must have a corresponding [Get value from cache](#GetFromCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bcd58-246">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="bcd58-246">Policy statement</span></span>  
  
```xml  
<cache-store-value key="cache key value" value="value to cache" duration="seconds" />  
```  
  
### <a name="example"></a><span data-ttu-id="bcd58-247">Örnek</span><span class="sxs-lookup"><span data-stu-id="bcd58-247">Example</span></span>  
 <span data-ttu-id="bcd58-248">Daha fazla bilgi ve bu ilkeyi örnekleri için bkz: [özel Azure API Management'te önbelleğe alma](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="bcd58-248">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="bcd58-249">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="bcd58-249">Elements</span></span>  
  
|<span data-ttu-id="bcd58-250">Ad</span><span class="sxs-lookup"><span data-stu-id="bcd58-250">Name</span></span>|<span data-ttu-id="bcd58-251">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bcd58-251">Description</span></span>|<span data-ttu-id="bcd58-252">Gerekli</span><span class="sxs-lookup"><span data-stu-id="bcd58-252">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="bcd58-253">Önbellek deposu değeri</span><span class="sxs-lookup"><span data-stu-id="bcd58-253">cache-store-value</span></span>|<span data-ttu-id="bcd58-254">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="bcd58-254">Root element.</span></span>|<span data-ttu-id="bcd58-255">Evet</span><span class="sxs-lookup"><span data-stu-id="bcd58-255">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bcd58-256">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="bcd58-256">Attributes</span></span>  
  
|<span data-ttu-id="bcd58-257">Ad</span><span class="sxs-lookup"><span data-stu-id="bcd58-257">Name</span></span>|<span data-ttu-id="bcd58-258">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bcd58-258">Description</span></span>|<span data-ttu-id="bcd58-259">Gerekli</span><span class="sxs-lookup"><span data-stu-id="bcd58-259">Required</span></span>|<span data-ttu-id="bcd58-260">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="bcd58-260">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="bcd58-261">Süre</span><span class="sxs-lookup"><span data-stu-id="bcd58-261">duration</span></span>|<span data-ttu-id="bcd58-262">Saniye cinsinden belirtilen sağlanan süre değeri için değer önbelleğe alınır.</span><span class="sxs-lookup"><span data-stu-id="bcd58-262">Value will be cached for the provided duration value, specified in seconds.</span></span>|<span data-ttu-id="bcd58-263">Evet</span><span class="sxs-lookup"><span data-stu-id="bcd58-263">Yes</span></span>|<span data-ttu-id="bcd58-264">Yok</span><span class="sxs-lookup"><span data-stu-id="bcd58-264">N/A</span></span>|  
|<span data-ttu-id="bcd58-265">anahtar</span><span class="sxs-lookup"><span data-stu-id="bcd58-265">key</span></span>|<span data-ttu-id="bcd58-266">Önbellek anahtarı değeri altında depolanır.</span><span class="sxs-lookup"><span data-stu-id="bcd58-266">Cache key the value will be stored under.</span></span>|<span data-ttu-id="bcd58-267">Evet</span><span class="sxs-lookup"><span data-stu-id="bcd58-267">Yes</span></span>|<span data-ttu-id="bcd58-268">Yok</span><span class="sxs-lookup"><span data-stu-id="bcd58-268">N/A</span></span>|  
|<span data-ttu-id="bcd58-269">değer</span><span class="sxs-lookup"><span data-stu-id="bcd58-269">value</span></span>|<span data-ttu-id="bcd58-270">Önbelleğe alınacak değer.</span><span class="sxs-lookup"><span data-stu-id="bcd58-270">The value to be cached.</span></span>|<span data-ttu-id="bcd58-271">Evet</span><span class="sxs-lookup"><span data-stu-id="bcd58-271">Yes</span></span>|<span data-ttu-id="bcd58-272">Yok</span><span class="sxs-lookup"><span data-stu-id="bcd58-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bcd58-273">Kullanım</span><span class="sxs-lookup"><span data-stu-id="bcd58-273">Usage</span></span>  
 <span data-ttu-id="bcd58-274">Bu ilke aşağıdaki ilkesi kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bcd58-274">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bcd58-275">**İlke bölümleri:** gelen, giden arka uç, hata</span><span class="sxs-lookup"><span data-stu-id="bcd58-275">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bcd58-276">**İlke kapsamları:** Genel API, işlemi, ürünü</span><span class="sxs-lookup"><span data-stu-id="bcd58-276">**Policy scopes:** global, API, operation, product</span></span>  
  
###  <span data-ttu-id="bcd58-277"><a name="RemoveCacheByKey"></a>Önbelleğe alınan değer Kaldır</span><span class="sxs-lookup"><span data-stu-id="bcd58-277"><a name="RemoveCacheByKey"></a> Remove value from cache</span></span>  
 <span data-ttu-id="bcd58-278">`cache-remove-value` Anahtara göre tanımlanan önbelleğe alınmış bir öğeyi siler.</span><span class="sxs-lookup"><span data-stu-id="bcd58-278">The             `cache-remove-value` deletes a cached item identified by its key.</span></span> <span data-ttu-id="bcd58-279">Anahtar isteğe bağlı bir dize değerine sahip olabilir ve genellikle bir ilke ifade kullanılarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="bcd58-279">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
#### <a name="policy-statement"></a><span data-ttu-id="bcd58-280">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="bcd58-280">Policy statement</span></span>  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="bcd58-281">Örnek</span><span class="sxs-lookup"><span data-stu-id="bcd58-281">Example</span></span>  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a><span data-ttu-id="bcd58-282">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="bcd58-282">Elements</span></span>  
  
|<span data-ttu-id="bcd58-283">Ad</span><span class="sxs-lookup"><span data-stu-id="bcd58-283">Name</span></span>|<span data-ttu-id="bcd58-284">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bcd58-284">Description</span></span>|<span data-ttu-id="bcd58-285">Gerekli</span><span class="sxs-lookup"><span data-stu-id="bcd58-285">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="bcd58-286">Önbellek Kaldır değeri</span><span class="sxs-lookup"><span data-stu-id="bcd58-286">cache-remove-value</span></span>|<span data-ttu-id="bcd58-287">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="bcd58-287">Root element.</span></span>|<span data-ttu-id="bcd58-288">Evet</span><span class="sxs-lookup"><span data-stu-id="bcd58-288">Yes</span></span>|  
  
#### <a name="attributes"></a><span data-ttu-id="bcd58-289">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="bcd58-289">Attributes</span></span>  
  
|<span data-ttu-id="bcd58-290">Ad</span><span class="sxs-lookup"><span data-stu-id="bcd58-290">Name</span></span>|<span data-ttu-id="bcd58-291">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bcd58-291">Description</span></span>|<span data-ttu-id="bcd58-292">Gerekli</span><span class="sxs-lookup"><span data-stu-id="bcd58-292">Required</span></span>|<span data-ttu-id="bcd58-293">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="bcd58-293">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="bcd58-294">anahtar</span><span class="sxs-lookup"><span data-stu-id="bcd58-294">key</span></span>|<span data-ttu-id="bcd58-295">Önbellekten kaldırılacak önceden önbelleğe alınan değerin anahtarı.</span><span class="sxs-lookup"><span data-stu-id="bcd58-295">The key of the previously cached value to be removed from the cache.</span></span>|<span data-ttu-id="bcd58-296">Evet</span><span class="sxs-lookup"><span data-stu-id="bcd58-296">Yes</span></span>|<span data-ttu-id="bcd58-297">Yok</span><span class="sxs-lookup"><span data-stu-id="bcd58-297">N/A</span></span>|  
  
#### <a name="usage"></a><span data-ttu-id="bcd58-298">Kullanım</span><span class="sxs-lookup"><span data-stu-id="bcd58-298">Usage</span></span>  
 <span data-ttu-id="bcd58-299">Bu ilke aşağıdaki ilkesi kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="bcd58-299">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="bcd58-300">**İlke bölümleri:** gelen, giden arka uç, hata</span><span class="sxs-lookup"><span data-stu-id="bcd58-300">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bcd58-301">**İlke kapsamları:** Genel API, işlemi, ürünü</span><span class="sxs-lookup"><span data-stu-id="bcd58-301">**Policy scopes:** global, API, operation, product</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="bcd58-302">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bcd58-302">Next steps</span></span>
<span data-ttu-id="bcd58-303">İlkeleriyle çalışma daha fazla bilgi için bkz: [API Management ilkeleri](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="bcd58-303">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  