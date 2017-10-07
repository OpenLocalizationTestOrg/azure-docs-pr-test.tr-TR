---
title: "aaaAzure API Management önbelleğe alma ilkeleri | Microsoft Docs"
description: "Önbelleğe alma ilkeleri için Azure API Management kullanılabilir hello hakkında bilgi edinin."
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
ms.openlocfilehash: bd6b0721945609b28dbf6e7ef0631979c08c8c65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-caching-policies"></a><span data-ttu-id="7c8bb-103">API Management önbelleğe alma ilkeleri</span><span class="sxs-lookup"><span data-stu-id="7c8bb-103">API Management caching policies</span></span>
<span data-ttu-id="7c8bb-104">Bu konuda API Management ilkelere hello için bir başvuru sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="7c8bb-105">Ekleme ve ilkeleri yapılandırma hakkında daha fazla bilgi için bkz: [API Management ilkeleri](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="7c8bb-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="7c8bb-106"><a name="CachingPolicies"></a>Önbelleğe alma ilkeleri</span><span class="sxs-lookup"><span data-stu-id="7c8bb-106"><a name="CachingPolicies"></a> Caching policies</span></span>  
  
-   <span data-ttu-id="7c8bb-107">Yanıt önbelleğe alma ilkeleri</span><span class="sxs-lookup"><span data-stu-id="7c8bb-107">Response caching policies</span></span>  
  
    -   <span data-ttu-id="7c8bb-108">[Önbellekten alma](api-management-caching-policies.md#GetFromCache) -önbellek gerçekleştirmek aramak ve geçerli bir önbelleğe alınan yanıtları kullanılabilir olduğunda döndürür.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-108">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached responses when available.</span></span>  
  
    -   <span data-ttu-id="7c8bb-109">[Depolama toocache](api-management-caching-policies.md#StoreToCache) - toohello belirtilen önbellek denetimi yapılandırma göre önbellekleri yanıtlar.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-109">[Store toocache](api-management-caching-policies.md#StoreToCache) - Caches responses according toohello specified cache control configuration.</span></span>  
  
-   <span data-ttu-id="7c8bb-110">Değer önbelleğe alma ilkeleri</span><span class="sxs-lookup"><span data-stu-id="7c8bb-110">Value caching policies</span></span>  
  
    -   <span data-ttu-id="7c8bb-111">[Önbelleğe alınan değer alma](#GetFromCacheByKey) -anahtar tarafından önbelleğe alınmış bir öğeyi geri almak.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-111">[Get value from cache](#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="7c8bb-112">[Değer önbellekte depolamak](#StoreToCacheByKey) -bir öğe anahtarı tarafından hello önbelleğine depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-112">[Store value in cache](#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>  
  
    -   <span data-ttu-id="7c8bb-113">[Önbelleğe alınan değer Kaldır](#RemoveCacheByKey) -öğeyi hello önbelleğinde anahtarının kaldırmak.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-113">[Remove value from cache](#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>  
  
##  <span data-ttu-id="7c8bb-114"><a name="GetFromCache"></a>Önbellekten alma</span><span class="sxs-lookup"><span data-stu-id="7c8bb-114"><a name="GetFromCache"></a> Get from cache</span></span>  
 <span data-ttu-id="7c8bb-115">Kullanım hello `cache-lookup` ilke tooperform önbelleği aramak ve geçerli bir önbelleğe alınan yanıt kullanılabilir olduğunda döndürür.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-115">Use hello `cache-lookup` policy tooperform cache look up and return a valid cached response when available.</span></span> <span data-ttu-id="7c8bb-116">Bu ilke, yanıt içeriği bir süre boyunca statik kalır olduğu durumlarda uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-116">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="7c8bb-117">Yanıt önbelleğe alma bant genişliğini azaltır ve işleme gereksinimlerini gecikmede API tüketiciler tarafından algılanan hello arka uç web sunucusu ve düşürmeye uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-117">Response caching reduces bandwidth and processing requirements imposed on hello backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="7c8bb-118">Bu ilke karşılık gelen olmalıdır [deposu toocache](api-management-caching-policies.md#StoreToCache) ilkesi.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-118">This policy must have a corresponding [Store toocache](api-management-caching-policies.md#StoreToCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="7c8bb-119">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="7c8bb-119">Policy statement</span></span>  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression tooevaluate)">  
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
  
### <a name="examples"></a><span data-ttu-id="7c8bb-120">Örnekler</span><span class="sxs-lookup"><span data-stu-id="7c8bb-120">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="7c8bb-121">Örnek</span><span class="sxs-lookup"><span data-stu-id="7c8bb-121">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="7c8bb-122">Örnek ilke ifadeleri kullanma</span><span class="sxs-lookup"><span data-stu-id="7c8bb-122">Example using policy expressions</span></span>  
 <span data-ttu-id="7c8bb-123">Bu örnek, hizmetin nasıl tootooconfigure API Management yanıt önbelleğe alma süresi eşleşmeleri hello belirtildiği gibi hello arka uç hizmetinin yanıt önbelleğe alma hello yedeklenen gösterir `Cache-Control` yönergesi.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-123">This example shows how tootooconfigure API Management response caching duration that matches hello response caching of hello backend service as specified by hello backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="7c8bb-124">Yapılandırma ve bu ilkeyi kullanan bir örnek için bkz: [bulut kapak bölüm 177: daha Vlad Vinogradsky ile yönetim özelliklerini API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) ve too25:25 ileri sarma.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-124">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too25:25.</span></span>  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="7c8bb-125">Daha fazla bilgi için bkz: [ilke ifadelerini](api-management-policy-expressions.md) ve [bağlamının](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="7c8bb-125">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="7c8bb-126">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="7c8bb-126">Elements</span></span>  
  
|<span data-ttu-id="7c8bb-127">Ad</span><span class="sxs-lookup"><span data-stu-id="7c8bb-127">Name</span></span>|<span data-ttu-id="7c8bb-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7c8bb-128">Description</span></span>|<span data-ttu-id="7c8bb-129">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7c8bb-129">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="7c8bb-130">Önbellek araması</span><span class="sxs-lookup"><span data-stu-id="7c8bb-130">cache-lookup</span></span>|<span data-ttu-id="7c8bb-131">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-131">Root element.</span></span>|<span data-ttu-id="7c8bb-132">Evet</span><span class="sxs-lookup"><span data-stu-id="7c8bb-132">Yes</span></span>|  
|<span data-ttu-id="7c8bb-133">farklılık tarafından-üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="7c8bb-133">vary-by-header</span></span>|<span data-ttu-id="7c8bb-134">Ana bilgisayardan kabul, Accept-Charset, Accept-Encoding, Accept-Language, yetkilendirme gibi Expect, belirtilen üstbilgi değerini başına yanıtlarını önbelleğe alma Başlat IF-Match.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-134">Start caching responses per value of specified header, such as Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span></span>|<span data-ttu-id="7c8bb-135">Hayır</span><span class="sxs-lookup"><span data-stu-id="7c8bb-135">No</span></span>|  
|<span data-ttu-id="7c8bb-136">farklılık-tarafından-query-parametresi</span><span class="sxs-lookup"><span data-stu-id="7c8bb-136">vary-by-query-parameter</span></span>|<span data-ttu-id="7c8bb-137">Her değeri belirtilen sorgu parametrelerinin yanıtlarını önbelleğe alma başlatın.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-137">Start caching responses per value of specified query parameters.</span></span> <span data-ttu-id="7c8bb-138">Tek bir veya birden çok parametre girin.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-138">Enter a single or multiple parameters.</span></span> <span data-ttu-id="7c8bb-139">Ayırıcı olarak virgül kullanın.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-139">Use semicolon as a separator.</span></span> <span data-ttu-id="7c8bb-140">Hiçbiri belirtilmezse, tüm sorgu parametreleri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-140">If none are specified, all query parameters are used.</span></span>|<span data-ttu-id="7c8bb-141">Hayır</span><span class="sxs-lookup"><span data-stu-id="7c8bb-141">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="7c8bb-142">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="7c8bb-142">Attributes</span></span>  
  
|<span data-ttu-id="7c8bb-143">Ad</span><span class="sxs-lookup"><span data-stu-id="7c8bb-143">Name</span></span>|<span data-ttu-id="7c8bb-144">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7c8bb-144">Description</span></span>|<span data-ttu-id="7c8bb-145">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7c8bb-145">Required</span></span>|<span data-ttu-id="7c8bb-146">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="7c8bb-146">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="7c8bb-147">izin ver-özel-yanıt-önbelleğe alma</span><span class="sxs-lookup"><span data-stu-id="7c8bb-147">allow-private-response-caching</span></span>|<span data-ttu-id="7c8bb-148">Ayarlandığında çok`true`, bir Authorization üstbilgisi içeren istekleri önbelleğe alma sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-148">When set too`true`, allows caching of requests that contain an Authorization header.</span></span>|<span data-ttu-id="7c8bb-149">Hayır</span><span class="sxs-lookup"><span data-stu-id="7c8bb-149">No</span></span>|<span data-ttu-id="7c8bb-150">False</span><span class="sxs-lookup"><span data-stu-id="7c8bb-150">false</span></span>|  
|<span data-ttu-id="7c8bb-151">önbelleğe alma aşağı akış türü</span><span class="sxs-lookup"><span data-stu-id="7c8bb-151">downstream-caching-type</span></span>|<span data-ttu-id="7c8bb-152">Bu öznitelik değerlerini aşağıdaki hello tooone ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-152">This attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="7c8bb-153">-none - aşağı akış önbelleğe alma izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-153">-   none - downstream caching is not allowed.</span></span><br /><span data-ttu-id="7c8bb-154">-Özel - aşağı akış özel önbelleğe alma izin verilir.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-154">-   private - downstream private caching is allowed.</span></span><br /><span data-ttu-id="7c8bb-155">-Genel - özel ve paylaşılan aşağı akış önbelleğe alma izin verilir.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-155">-   public - private and shared downstream caching is allowed.</span></span>|<span data-ttu-id="7c8bb-156">Hayır</span><span class="sxs-lookup"><span data-stu-id="7c8bb-156">No</span></span>|<span data-ttu-id="7c8bb-157">Yok</span><span class="sxs-lookup"><span data-stu-id="7c8bb-157">none</span></span>|  
|<span data-ttu-id="7c8bb-158">gereken revalidate</span><span class="sxs-lookup"><span data-stu-id="7c8bb-158">must-revalidate</span></span>|<span data-ttu-id="7c8bb-159">Aşağı Akış önbelleği etkin olduğunda, bu öznitelik açar veya hello kapatır `must-revalidate` ağ geçidi yanıtlarındaki önbellek denetimi yönergesi.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-159">When downstream caching is enabled this attribute turns on or off  hello `must-revalidate` cache control directive in gateway responses.</span></span>|<span data-ttu-id="7c8bb-160">Hayır</span><span class="sxs-lookup"><span data-stu-id="7c8bb-160">No</span></span>|<span data-ttu-id="7c8bb-161">TRUE</span><span class="sxs-lookup"><span data-stu-id="7c8bb-161">true</span></span>|  
|<span data-ttu-id="7c8bb-162">farklılık-tarafından-Geliştirici</span><span class="sxs-lookup"><span data-stu-id="7c8bb-162">vary-by-developer</span></span>|<span data-ttu-id="7c8bb-163">Çok ayarlamak`true` Geliştirici anahtar başına toocache yanıtlar.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-163">Set too`true` toocache responses per developer key.</span></span>|<span data-ttu-id="7c8bb-164">Hayır</span><span class="sxs-lookup"><span data-stu-id="7c8bb-164">No</span></span>|<span data-ttu-id="7c8bb-165">False</span><span class="sxs-lookup"><span data-stu-id="7c8bb-165">false</span></span>|  
|<span data-ttu-id="7c8bb-166">farklılık tarafından-Geliştirici-grupları</span><span class="sxs-lookup"><span data-stu-id="7c8bb-166">vary-by-developer-groups</span></span>|<span data-ttu-id="7c8bb-167">Çok ayarlamak`true` kullanıcı rol başına toocache yanıtlar.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-167">Set too`true` toocache responses per user role.</span></span>|<span data-ttu-id="7c8bb-168">Hayır</span><span class="sxs-lookup"><span data-stu-id="7c8bb-168">No</span></span>|<span data-ttu-id="7c8bb-169">False</span><span class="sxs-lookup"><span data-stu-id="7c8bb-169">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="7c8bb-170">Kullanım</span><span class="sxs-lookup"><span data-stu-id="7c8bb-170">Usage</span></span>  
 <span data-ttu-id="7c8bb-171">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="7c8bb-171">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="7c8bb-172">**İlke bölümleri:** gelen</span><span class="sxs-lookup"><span data-stu-id="7c8bb-172">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="7c8bb-173">**İlke kapsamları:** API işlemi, ürün</span><span class="sxs-lookup"><span data-stu-id="7c8bb-173">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="7c8bb-174"><a name="StoreToCache"></a>Depolama toocache</span><span class="sxs-lookup"><span data-stu-id="7c8bb-174"><a name="StoreToCache"></a> Store toocache</span></span>  
 <span data-ttu-id="7c8bb-175">Merhaba `cache-store` toohello göre ilke önbellekleri yanıtları belirtilen önbellek ayarları.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-175">hello `cache-store` policy caches responses according toohello specified cache settings.</span></span> <span data-ttu-id="7c8bb-176">Bu ilke, yanıt içeriği bir süre boyunca statik kalır olduğu durumlarda uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-176">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="7c8bb-177">Yanıt önbelleğe alma bant genişliğini azaltır ve işleme gereksinimlerini gecikmede API tüketiciler tarafından algılanan hello arka uç web sunucusu ve düşürmeye uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-177">Response caching reduces bandwidth and processing requirements imposed on hello backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="7c8bb-178">Bu ilke karşılık gelen olmalıdır [önbellekten alma](api-management-caching-policies.md#GetFromCache) ilkesi.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-178">This policy must have a corresponding [Get from cache](api-management-caching-policies.md#GetFromCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="7c8bb-179">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="7c8bb-179">Policy statement</span></span>  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a><span data-ttu-id="7c8bb-180">Örnekler</span><span class="sxs-lookup"><span data-stu-id="7c8bb-180">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="7c8bb-181">Örnek</span><span class="sxs-lookup"><span data-stu-id="7c8bb-181">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="7c8bb-182">Örnek ilke ifadeleri kullanma</span><span class="sxs-lookup"><span data-stu-id="7c8bb-182">Example using policy expressions</span></span>  
 <span data-ttu-id="7c8bb-183">Bu örnek, hizmetin nasıl tootooconfigure API Management yanıt önbelleğe alma süresi eşleşmeleri hello belirtildiği gibi hello arka uç hizmetinin yanıt önbelleğe alma hello yedeklenen gösterir `Cache-Control` yönergesi.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-183">This example shows how tootooconfigure API Management response caching duration that matches hello response caching of hello backend service as specified by hello backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="7c8bb-184">Yapılandırma ve bu ilkeyi kullanan bir örnek için bkz: [bulut kapak bölüm 177: daha Vlad Vinogradsky ile yönetim özelliklerini API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) ve too25:25 ileri sarma.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-184">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too25:25.</span></span>  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="7c8bb-185">Daha fazla bilgi için bkz: [ilke ifadelerini](api-management-policy-expressions.md) ve [bağlamının](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="7c8bb-185">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="7c8bb-186">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="7c8bb-186">Elements</span></span>  
  
|<span data-ttu-id="7c8bb-187">Ad</span><span class="sxs-lookup"><span data-stu-id="7c8bb-187">Name</span></span>|<span data-ttu-id="7c8bb-188">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7c8bb-188">Description</span></span>|<span data-ttu-id="7c8bb-189">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7c8bb-189">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="7c8bb-190">Önbellek deposu</span><span class="sxs-lookup"><span data-stu-id="7c8bb-190">cache-store</span></span>|<span data-ttu-id="7c8bb-191">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-191">Root element.</span></span>|<span data-ttu-id="7c8bb-192">Evet</span><span class="sxs-lookup"><span data-stu-id="7c8bb-192">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="7c8bb-193">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="7c8bb-193">Attributes</span></span>  
  
|<span data-ttu-id="7c8bb-194">Ad</span><span class="sxs-lookup"><span data-stu-id="7c8bb-194">Name</span></span>|<span data-ttu-id="7c8bb-195">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7c8bb-195">Description</span></span>|<span data-ttu-id="7c8bb-196">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7c8bb-196">Required</span></span>|<span data-ttu-id="7c8bb-197">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="7c8bb-197">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="7c8bb-198">Süre</span><span class="sxs-lookup"><span data-stu-id="7c8bb-198">duration</span></span>|<span data-ttu-id="7c8bb-199">Time-to-live Merhaba, saniye cinsinden belirtilen girişleri, önbelleğe alınmış.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-199">Time-to-live of hello cached entries, specified in seconds.</span></span>|<span data-ttu-id="7c8bb-200">Evet</span><span class="sxs-lookup"><span data-stu-id="7c8bb-200">Yes</span></span>|<span data-ttu-id="7c8bb-201">Yok</span><span class="sxs-lookup"><span data-stu-id="7c8bb-201">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="7c8bb-202">Kullanım</span><span class="sxs-lookup"><span data-stu-id="7c8bb-202">Usage</span></span>  
 <span data-ttu-id="7c8bb-203">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="7c8bb-203">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="7c8bb-204">**İlke bölümleri:** giden</span><span class="sxs-lookup"><span data-stu-id="7c8bb-204">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="7c8bb-205">**İlke kapsamları:** API işlemi, ürün</span><span class="sxs-lookup"><span data-stu-id="7c8bb-205">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="7c8bb-206"><a name="GetFromCacheByKey"></a>Önbelleğe alınan değer alma</span><span class="sxs-lookup"><span data-stu-id="7c8bb-206"><a name="GetFromCacheByKey"></a> Get value from cache</span></span>  
 <span data-ttu-id="7c8bb-207">Kullanım hello `cache-lookup-value` İlkesi tooperform arama anahtar tarafından önbelleğe ve önbelleğe alınan değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-207">Use hello `cache-lookup-value` policy tooperform cache lookup by key and return a cached value.</span></span> <span data-ttu-id="7c8bb-208">Merhaba anahtar bir isteğe bağlı bir dize değerine sahip olabilir ve genellikle bir ilke ifade kullanılarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-208">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="7c8bb-209">Bu ilke karşılık gelen olmalıdır [değeri önbellekte depolamak](#StoreToCacheByKey) ilkesi.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-209">This policy must have a corresponding [Store value in cache](#StoreToCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="7c8bb-210">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="7c8bb-210">Policy statement</span></span>  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value toouse if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a><span data-ttu-id="7c8bb-211">Örnek</span><span class="sxs-lookup"><span data-stu-id="7c8bb-211">Example</span></span>  
 <span data-ttu-id="7c8bb-212">Daha fazla bilgi ve bu ilkeyi örnekleri için bkz: [özel Azure API Management'te önbelleğe alma](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="7c8bb-212">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="7c8bb-213">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="7c8bb-213">Elements</span></span>  
  
|<span data-ttu-id="7c8bb-214">Ad</span><span class="sxs-lookup"><span data-stu-id="7c8bb-214">Name</span></span>|<span data-ttu-id="7c8bb-215">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7c8bb-215">Description</span></span>|<span data-ttu-id="7c8bb-216">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7c8bb-216">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="7c8bb-217">Önbellek arama değeri</span><span class="sxs-lookup"><span data-stu-id="7c8bb-217">cache-lookup-value</span></span>|<span data-ttu-id="7c8bb-218">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-218">Root element.</span></span>|<span data-ttu-id="7c8bb-219">Evet</span><span class="sxs-lookup"><span data-stu-id="7c8bb-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="7c8bb-220">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="7c8bb-220">Attributes</span></span>  
  
|<span data-ttu-id="7c8bb-221">Ad</span><span class="sxs-lookup"><span data-stu-id="7c8bb-221">Name</span></span>|<span data-ttu-id="7c8bb-222">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7c8bb-222">Description</span></span>|<span data-ttu-id="7c8bb-223">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7c8bb-223">Required</span></span>|<span data-ttu-id="7c8bb-224">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="7c8bb-224">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="7c8bb-225">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="7c8bb-225">default-value</span></span>|<span data-ttu-id="7c8bb-226">Merhaba önbellek anahtar arama bir isabetsizliği oluştuysa toohello değişkeni atanacak bir değer.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-226">A value that will be assigned toohello variable if hello cache key lookup resulted in a miss.</span></span> <span data-ttu-id="7c8bb-227">Bu özniteliği belirtilmezse, `null` atanır.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-227">If this attribute is not specified, `null` is assigned.</span></span>|<span data-ttu-id="7c8bb-228">Hayır</span><span class="sxs-lookup"><span data-stu-id="7c8bb-228">No</span></span>|`null`|  
|<span data-ttu-id="7c8bb-229">anahtar</span><span class="sxs-lookup"><span data-stu-id="7c8bb-229">key</span></span>|<span data-ttu-id="7c8bb-230">Anahtar değeri toouse hello aramada önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-230">Cache key value toouse in hello lookup.</span></span>|<span data-ttu-id="7c8bb-231">Evet</span><span class="sxs-lookup"><span data-stu-id="7c8bb-231">Yes</span></span>|<span data-ttu-id="7c8bb-232">Yok</span><span class="sxs-lookup"><span data-stu-id="7c8bb-232">N/A</span></span>|  
|<span data-ttu-id="7c8bb-233">değişken adı</span><span class="sxs-lookup"><span data-stu-id="7c8bb-233">variable-name</span></span>|<span data-ttu-id="7c8bb-234">Merhaba adını [bağlamının](api-management-policy-expressions.md#ContextVariables) değeri Aranan hello atanacak için arama başarılı olduğunda.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-234">Name of hello [context variable](api-management-policy-expressions.md#ContextVariables) hello looked up value will be assigned to, if lookup is successful.</span></span> <span data-ttu-id="7c8bb-235">Arama bir isabetsizliği sonuçlanırsa hello değişkeni hello hello değeri atanacak `default-value` özniteliği veya `null`Merhaba, `default-value` özniteliği atlanmış.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-235">If lookup results in a miss, hello variable will be assigned hello value of hello `default-value` attribute or `null`, if hello `default-value` attribute is omitted.</span></span>|<span data-ttu-id="7c8bb-236">Evet</span><span class="sxs-lookup"><span data-stu-id="7c8bb-236">Yes</span></span>|<span data-ttu-id="7c8bb-237">Yok</span><span class="sxs-lookup"><span data-stu-id="7c8bb-237">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="7c8bb-238">Kullanım</span><span class="sxs-lookup"><span data-stu-id="7c8bb-238">Usage</span></span>  
 <span data-ttu-id="7c8bb-239">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="7c8bb-239">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="7c8bb-240">**İlke bölümleri:** gelen, giden arka uç, hata</span><span class="sxs-lookup"><span data-stu-id="7c8bb-240">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="7c8bb-241">**İlke kapsamları:** Genel API, işlemi, ürünü</span><span class="sxs-lookup"><span data-stu-id="7c8bb-241">**Policy scopes:** global, API, operation, product</span></span>  
  
##  <span data-ttu-id="7c8bb-242"><a name="StoreToCacheByKey"></a>Önbellek deposu değeri</span><span class="sxs-lookup"><span data-stu-id="7c8bb-242"><a name="StoreToCacheByKey"></a> Store value in cache</span></span>  
 <span data-ttu-id="7c8bb-243">Merhaba `cache-store-value` önbellek depolama anahtarının gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-243">hello `cache-store-value` performs cache storage by key.</span></span> <span data-ttu-id="7c8bb-244">Merhaba anahtar bir isteğe bağlı bir dize değerine sahip olabilir ve genellikle bir ilke ifade kullanılarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-244">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="7c8bb-245">Bu ilke karşılık gelen olmalıdır [değeri önbellekten alma](#GetFromCacheByKey) ilkesi.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-245">This policy must have a corresponding [Get value from cache](#GetFromCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="7c8bb-246">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="7c8bb-246">Policy statement</span></span>  
  
```xml  
<cache-store-value key="cache key value" value="value toocache" duration="seconds" />  
```  
  
### <a name="example"></a><span data-ttu-id="7c8bb-247">Örnek</span><span class="sxs-lookup"><span data-stu-id="7c8bb-247">Example</span></span>  
 <span data-ttu-id="7c8bb-248">Daha fazla bilgi ve bu ilkeyi örnekleri için bkz: [özel Azure API Management'te önbelleğe alma](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="7c8bb-248">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="7c8bb-249">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="7c8bb-249">Elements</span></span>  
  
|<span data-ttu-id="7c8bb-250">Ad</span><span class="sxs-lookup"><span data-stu-id="7c8bb-250">Name</span></span>|<span data-ttu-id="7c8bb-251">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7c8bb-251">Description</span></span>|<span data-ttu-id="7c8bb-252">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7c8bb-252">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="7c8bb-253">Önbellek deposu değeri</span><span class="sxs-lookup"><span data-stu-id="7c8bb-253">cache-store-value</span></span>|<span data-ttu-id="7c8bb-254">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-254">Root element.</span></span>|<span data-ttu-id="7c8bb-255">Evet</span><span class="sxs-lookup"><span data-stu-id="7c8bb-255">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="7c8bb-256">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="7c8bb-256">Attributes</span></span>  
  
|<span data-ttu-id="7c8bb-257">Ad</span><span class="sxs-lookup"><span data-stu-id="7c8bb-257">Name</span></span>|<span data-ttu-id="7c8bb-258">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7c8bb-258">Description</span></span>|<span data-ttu-id="7c8bb-259">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7c8bb-259">Required</span></span>|<span data-ttu-id="7c8bb-260">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="7c8bb-260">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="7c8bb-261">Süre</span><span class="sxs-lookup"><span data-stu-id="7c8bb-261">duration</span></span>|<span data-ttu-id="7c8bb-262">Saniye cinsinden belirtilen süre değerinin sağlanan hello için değer önbelleğe alınır.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-262">Value will be cached for hello provided duration value, specified in seconds.</span></span>|<span data-ttu-id="7c8bb-263">Evet</span><span class="sxs-lookup"><span data-stu-id="7c8bb-263">Yes</span></span>|<span data-ttu-id="7c8bb-264">Yok</span><span class="sxs-lookup"><span data-stu-id="7c8bb-264">N/A</span></span>|  
|<span data-ttu-id="7c8bb-265">anahtar</span><span class="sxs-lookup"><span data-stu-id="7c8bb-265">key</span></span>|<span data-ttu-id="7c8bb-266">Önbellek anahtar hello değeri altında depolanır.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-266">Cache key hello value will be stored under.</span></span>|<span data-ttu-id="7c8bb-267">Evet</span><span class="sxs-lookup"><span data-stu-id="7c8bb-267">Yes</span></span>|<span data-ttu-id="7c8bb-268">Yok</span><span class="sxs-lookup"><span data-stu-id="7c8bb-268">N/A</span></span>|  
|<span data-ttu-id="7c8bb-269">değer</span><span class="sxs-lookup"><span data-stu-id="7c8bb-269">value</span></span>|<span data-ttu-id="7c8bb-270">Merhaba değeri toobe önbelleğe alınmış.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-270">hello value toobe cached.</span></span>|<span data-ttu-id="7c8bb-271">Evet</span><span class="sxs-lookup"><span data-stu-id="7c8bb-271">Yes</span></span>|<span data-ttu-id="7c8bb-272">Yok</span><span class="sxs-lookup"><span data-stu-id="7c8bb-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="7c8bb-273">Kullanım</span><span class="sxs-lookup"><span data-stu-id="7c8bb-273">Usage</span></span>  
 <span data-ttu-id="7c8bb-274">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="7c8bb-274">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="7c8bb-275">**İlke bölümleri:** gelen, giden arka uç, hata</span><span class="sxs-lookup"><span data-stu-id="7c8bb-275">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="7c8bb-276">**İlke kapsamları:** Genel API, işlemi, ürünü</span><span class="sxs-lookup"><span data-stu-id="7c8bb-276">**Policy scopes:** global, API, operation, product</span></span>  
  
###  <span data-ttu-id="7c8bb-277"><a name="RemoveCacheByKey"></a>Önbelleğe alınan değer Kaldır</span><span class="sxs-lookup"><span data-stu-id="7c8bb-277"><a name="RemoveCacheByKey"></a> Remove value from cache</span></span>  
 <span data-ttu-id="7c8bb-278">Merhaba `cache-remove-value` anahtara göre tanımlanan önbelleğe alınmış bir öğeyi siler.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-278">hello             `cache-remove-value` deletes a cached item identified by its key.</span></span> <span data-ttu-id="7c8bb-279">Merhaba anahtar bir isteğe bağlı bir dize değerine sahip olabilir ve genellikle bir ilke ifade kullanılarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-279">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
#### <a name="policy-statement"></a><span data-ttu-id="7c8bb-280">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="7c8bb-280">Policy statement</span></span>  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="7c8bb-281">Örnek</span><span class="sxs-lookup"><span data-stu-id="7c8bb-281">Example</span></span>  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a><span data-ttu-id="7c8bb-282">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="7c8bb-282">Elements</span></span>  
  
|<span data-ttu-id="7c8bb-283">Ad</span><span class="sxs-lookup"><span data-stu-id="7c8bb-283">Name</span></span>|<span data-ttu-id="7c8bb-284">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7c8bb-284">Description</span></span>|<span data-ttu-id="7c8bb-285">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7c8bb-285">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="7c8bb-286">Önbellek Kaldır değeri</span><span class="sxs-lookup"><span data-stu-id="7c8bb-286">cache-remove-value</span></span>|<span data-ttu-id="7c8bb-287">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-287">Root element.</span></span>|<span data-ttu-id="7c8bb-288">Evet</span><span class="sxs-lookup"><span data-stu-id="7c8bb-288">Yes</span></span>|  
  
#### <a name="attributes"></a><span data-ttu-id="7c8bb-289">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="7c8bb-289">Attributes</span></span>  
  
|<span data-ttu-id="7c8bb-290">Ad</span><span class="sxs-lookup"><span data-stu-id="7c8bb-290">Name</span></span>|<span data-ttu-id="7c8bb-291">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7c8bb-291">Description</span></span>|<span data-ttu-id="7c8bb-292">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7c8bb-292">Required</span></span>|<span data-ttu-id="7c8bb-293">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="7c8bb-293">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="7c8bb-294">anahtar</span><span class="sxs-lookup"><span data-stu-id="7c8bb-294">key</span></span>|<span data-ttu-id="7c8bb-295">Merhaba Hello anahtarı değeri toobe hello önbellekten kaldırıldı daha önce önbelleğe alınmış.</span><span class="sxs-lookup"><span data-stu-id="7c8bb-295">hello key of hello previously cached value toobe removed from hello cache.</span></span>|<span data-ttu-id="7c8bb-296">Evet</span><span class="sxs-lookup"><span data-stu-id="7c8bb-296">Yes</span></span>|<span data-ttu-id="7c8bb-297">Yok</span><span class="sxs-lookup"><span data-stu-id="7c8bb-297">N/A</span></span>|  
  
#### <a name="usage"></a><span data-ttu-id="7c8bb-298">Kullanım</span><span class="sxs-lookup"><span data-stu-id="7c8bb-298">Usage</span></span>  
 <span data-ttu-id="7c8bb-299">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="7c8bb-299">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="7c8bb-300">**İlke bölümleri:** gelen, giden arka uç, hata</span><span class="sxs-lookup"><span data-stu-id="7c8bb-300">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="7c8bb-301">**İlke kapsamları:** Genel API, işlemi, ürünü</span><span class="sxs-lookup"><span data-stu-id="7c8bb-301">**Policy scopes:** global, API, operation, product</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="7c8bb-302">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7c8bb-302">Next steps</span></span>
<span data-ttu-id="7c8bb-303">İlkeleriyle çalışma daha fazla bilgi için bkz: [API Management ilkeleri](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="7c8bb-303">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  