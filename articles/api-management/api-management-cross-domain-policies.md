---
title: "etki alanları arası ilkeler aaaAzure API Management | Microsoft Docs"
description: "Etki alanları arası ilkeler Azure API Management'te kullanıma hello hakkında bilgi edinin."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7689d277-8abe-472a-a78c-e6d4bd43455d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: dd5ebfd65b92ebd0c1f589a2bac669a3928d40b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-cross-domain-policies"></a><span data-ttu-id="c2df1-103">API Management etki alanları arası ilkeler</span><span class="sxs-lookup"><span data-stu-id="c2df1-103">API Management cross domain policies</span></span>
<span data-ttu-id="c2df1-104">Bu konuda API Management ilkelere hello için bir başvuru sağlar.</span><span class="sxs-lookup"><span data-stu-id="c2df1-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="c2df1-105">Ekleme ve ilkeleri yapılandırma hakkında daha fazla bilgi için bkz: [API Management ilkeleri](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="c2df1-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="c2df1-106"><a name="CrossDomainPolicies"></a>Etki alanı ilkelerini arası</span><span class="sxs-lookup"><span data-stu-id="c2df1-106"><a name="CrossDomainPolicies"></a> Cross domain policies</span></span>  
  
-   <span data-ttu-id="c2df1-107">[Etki alanları arası çağrılar izin](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -yapar hello API erişilebilir Microsoft Silverlight Adobe Flash ve tarayıcı tabanlı istemcilerden.</span><span class="sxs-lookup"><span data-stu-id="c2df1-107">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
-   <span data-ttu-id="c2df1-108">[CORS](api-management-cross-domain-policies.md#CORS) -çıkış noktaları arası kaynak paylaşımını (CORS) tooan işlemi destekler veya bir API tooallow etki alanları arası tarayıcı tabanlı istemcilerden çağıran ekler.</span><span class="sxs-lookup"><span data-stu-id="c2df1-108">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
-   <span data-ttu-id="c2df1-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - JSON ile destek tooan işlemi (JSONP) doldurma ekler veya bir API tooallow etki alanları arası JavaScript tarayıcı tabanlı istemcilerden çağırır.</span><span class="sxs-lookup"><span data-stu-id="c2df1-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
##  <span data-ttu-id="c2df1-110"><a name="AllowCrossDomainCalls"></a>Etki alanları arası çağrılar izin ver</span><span class="sxs-lookup"><span data-stu-id="c2df1-110"><a name="AllowCrossDomainCalls"></a> Allow cross-domain calls</span></span>  
 <span data-ttu-id="c2df1-111">Kullanım hello `cross-domain` İlkesi toomake hello API Adobe Flash ve Microsoft Silverlight tarayıcı tabanlı istemcilerden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="c2df1-111">Use hello `cross-domain` policy toomake hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c2df1-112">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="c2df1-112">Policy statement</span></span>  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in hello Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a><span data-ttu-id="c2df1-113">Örnek</span><span class="sxs-lookup"><span data-stu-id="c2df1-113">Example</span></span>  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a><span data-ttu-id="c2df1-114">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="c2df1-114">Elements</span></span>  
  
|<span data-ttu-id="c2df1-115">Ad</span><span class="sxs-lookup"><span data-stu-id="c2df1-115">Name</span></span>|<span data-ttu-id="c2df1-116">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c2df1-116">Description</span></span>|<span data-ttu-id="c2df1-117">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c2df1-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c2df1-118">etki alanları arası</span><span class="sxs-lookup"><span data-stu-id="c2df1-118">cross-domain</span></span>|<span data-ttu-id="c2df1-119">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="c2df1-119">Root element.</span></span> <span data-ttu-id="c2df1-120">Alt öğeler toohello uygun olmalıdır [Adobe etki alanları arası ilke dosya belirtimi](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span><span class="sxs-lookup"><span data-stu-id="c2df1-120">Child elements must conform toohello [Adobe cross-domain policy file specification](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span></span>|<span data-ttu-id="c2df1-121">Evet</span><span class="sxs-lookup"><span data-stu-id="c2df1-121">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c2df1-122">Kullanım</span><span class="sxs-lookup"><span data-stu-id="c2df1-122">Usage</span></span>  
 <span data-ttu-id="c2df1-123">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c2df1-123">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c2df1-124">**İlke bölümleri:** gelen</span><span class="sxs-lookup"><span data-stu-id="c2df1-124">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="c2df1-125">**İlke kapsamları:** genel</span><span class="sxs-lookup"><span data-stu-id="c2df1-125">**Policy scopes:** global</span></span>  
  
##  <span data-ttu-id="c2df1-126"><a name="CORS"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="c2df1-126"><a name="CORS"></a> CORS</span></span>  
 <span data-ttu-id="c2df1-127">Merhaba `cors` ilkesi ekler çıkış noktaları arası kaynak paylaşımını (CORS) tooan işlemi destekler veya bir API tooallow etki alanları arası tarayıcı tabanlı istemcilerden çağırır.</span><span class="sxs-lookup"><span data-stu-id="c2df1-127">hello `cors` policy adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
 <span data-ttu-id="c2df1-128">CORS tooallow belirli çıkış noktaları arası (bir web sayfası tooother etki alanları JavaScript yapılan yani XMLHttpRequests çağrıları) isteklerini olup olmadığını belirlemek ve bir tarayıcı ve sunucu toointeract sağlar.</span><span class="sxs-lookup"><span data-stu-id="c2df1-128">CORS allows a browser and a server toointeract and determine whether or not tooallow specific cross-origin requests (i.e. XMLHttpRequests calls made from JavaScript on a web page tooother domains).</span></span> <span data-ttu-id="c2df1-129">Bu, yalnızca kaynak aynı isteklerine izin'den daha fazla esneklik sağlar, ancak tüm çıkış noktaları arası istekleri izin vererek değerinden daha güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="c2df1-129">This allows for more flexibility than only allowing same-origin requests, but is more secure than allowing all cross-origin requests.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c2df1-130">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="c2df1-130">Policy statement</span></span>  
  
```xml  
<cors allow-credentials="false|true">  
    <allowed-origins>  
        <origin>origin uri</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="number of seconds">  
        <method>http verb</method>  
    </allowed-methods>  
    <allowed-headers>  
        <header>header name</header>  
    </allowed-headers>  
    <expose-headers>  
        <header>header name</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="example"></a><span data-ttu-id="c2df1-131">Örnek</span><span class="sxs-lookup"><span data-stu-id="c2df1-131">Example</span></span>  
 <span data-ttu-id="c2df1-132">Bu örnek nasıl toosupport öncesi uçuş, özel üstbilgi veya dışında GET ve POST yöntemleri olanlar gibi istekleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="c2df1-132">This example demonstrates how toosupport pre-flight requests, such as those with custom headers or methods other than GET and POST.</span></span> <span data-ttu-id="c2df1-133">toosupport özel üstbilgi ve ek HTTP fiilleri kullanın hello `allowed-methods` ve `allowed-headers` bölümler hello aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="c2df1-133">toosupport custom headers and additional HTTP verbs, use hello `allowed-methods` and `allowed-headers` sections as shown in hello following example.</span></span>  
  
```xml  
<cors allow-credentials="true">  
    <allowed-origins>  
        <!-- Localhost useful for development -->  
        <origin>http://localhost:8080/</origin>  
        <origin>http://example.com/</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="300">  
        <method>GET</method>  
        <method>POST</method>  
        <method>PATCH</method>  
        <method>DELETE</method>  
    </allowed-methods>  
    <allowed-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
        <header>x-zumo-version</header>  
        <header>x-zumo-auth</header>  
        <header>content-type</header>  
        <header>accept</header>  
    </allowed-headers>  
    <expose-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="elements"></a><span data-ttu-id="c2df1-134">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="c2df1-134">Elements</span></span>  
  
|<span data-ttu-id="c2df1-135">Ad</span><span class="sxs-lookup"><span data-stu-id="c2df1-135">Name</span></span>|<span data-ttu-id="c2df1-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c2df1-136">Description</span></span>|<span data-ttu-id="c2df1-137">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c2df1-137">Required</span></span>|<span data-ttu-id="c2df1-138">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="c2df1-138">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c2df1-139">cors</span><span class="sxs-lookup"><span data-stu-id="c2df1-139">cors</span></span>|<span data-ttu-id="c2df1-140">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="c2df1-140">Root element.</span></span>|<span data-ttu-id="c2df1-141">Evet</span><span class="sxs-lookup"><span data-stu-id="c2df1-141">Yes</span></span>|<span data-ttu-id="c2df1-142">Yok</span><span class="sxs-lookup"><span data-stu-id="c2df1-142">N/A</span></span>|  
|<span data-ttu-id="c2df1-143">izin verilen çıkış</span><span class="sxs-lookup"><span data-stu-id="c2df1-143">allowed-origins</span></span>|<span data-ttu-id="c2df1-144">İçeren `origin` çıkış noktası etki alanları arası istekleri için izin verilen hello açıklayan öğeler.</span><span class="sxs-lookup"><span data-stu-id="c2df1-144">Contains `origin` elements that describe hello allowed origins for cross-domain requests.</span></span> <span data-ttu-id="c2df1-145">`allowed-origins`ya da tek bir içerebilir `origin` belirtir öğesi `*` tooallow her türlü kaynağa veya bir veya daha fazla `origin` bir URI içeren öğeler.</span><span class="sxs-lookup"><span data-stu-id="c2df1-145">`allowed-origins` can contain either a single `origin` element that specifies `*` tooallow any origin, or one or more `origin` elements that contain a URI.</span></span>|<span data-ttu-id="c2df1-146">Evet</span><span class="sxs-lookup"><span data-stu-id="c2df1-146">Yes</span></span>|<span data-ttu-id="c2df1-147">Yok</span><span class="sxs-lookup"><span data-stu-id="c2df1-147">N/A</span></span>|  
|<span data-ttu-id="c2df1-148">Kaynak</span><span class="sxs-lookup"><span data-stu-id="c2df1-148">origin</span></span>|<span data-ttu-id="c2df1-149">Merhaba değer ya da olabilir `*` tooallow tüm kaynaklara ya da tek bir kaynak belirten bir URI.</span><span class="sxs-lookup"><span data-stu-id="c2df1-149">hello value can be either `*` tooallow all origins, or a URI that specifies a single origin.</span></span> <span data-ttu-id="c2df1-150">Merhaba URI düzeni, ana bilgisayar ve bağlantı noktası eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c2df1-150">hello URI must include a scheme, host, and port.</span></span>|<span data-ttu-id="c2df1-151">Evet</span><span class="sxs-lookup"><span data-stu-id="c2df1-151">Yes</span></span>|<span data-ttu-id="c2df1-152">Başlangıç bağlantı noktası bir URI atlanırsa, HTTP için 80 numaralı bağlantı noktası kullanılır ve HTTPS için 443 numaralı bağlantı noktası kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c2df1-152">If hello port is omitted in a URI, port 80 is used for HTTP and port 443 is used for HTTPS.</span></span>|  
|<span data-ttu-id="c2df1-153">izin verilen yöntemleri</span><span class="sxs-lookup"><span data-stu-id="c2df1-153">allowed-methods</span></span>|<span data-ttu-id="c2df1-154">Yöntemleri dışında GET veya POST izin verilir, bu öğe gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c2df1-154">This element is required if methods other than GET or POST are allowed.</span></span> <span data-ttu-id="c2df1-155">İçeren `method` hello desteklenen HTTP fiilleri belirtin öğeleri.</span><span class="sxs-lookup"><span data-stu-id="c2df1-155">Contains `method` elements that specify hello supported HTTP verbs.</span></span>|<span data-ttu-id="c2df1-156">Hayır</span><span class="sxs-lookup"><span data-stu-id="c2df1-156">No</span></span>|<span data-ttu-id="c2df1-157">Bu bölümde mevcut değilse, GET ve POST desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c2df1-157">If this section is not present, GET and POST are supported.</span></span>|  
|<span data-ttu-id="c2df1-158">Yöntemi</span><span class="sxs-lookup"><span data-stu-id="c2df1-158">method</span></span>|<span data-ttu-id="c2df1-159">Bir HTTP fiili belirtir.</span><span class="sxs-lookup"><span data-stu-id="c2df1-159">Specifies an HTTP verb.</span></span>|<span data-ttu-id="c2df1-160">En az bir `method` öğesi olup gerekli hello `allowed-methods` bölüm mevcut.</span><span class="sxs-lookup"><span data-stu-id="c2df1-160">At least one `method` element is required if hello `allowed-methods` section is present.</span></span>|<span data-ttu-id="c2df1-161">Yok</span><span class="sxs-lookup"><span data-stu-id="c2df1-161">N/A</span></span>|  
|<span data-ttu-id="c2df1-162">izin verilen üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="c2df1-162">allowed-headers</span></span>|<span data-ttu-id="c2df1-163">Bu öğeyi içeren `header` öğeleri hello isteğine dahil hello başlıklarının adlarını belirtme.</span><span class="sxs-lookup"><span data-stu-id="c2df1-163">This element contains `header` elements specifying names of hello headers that can be included in hello request.</span></span>|<span data-ttu-id="c2df1-164">Hayır</span><span class="sxs-lookup"><span data-stu-id="c2df1-164">No</span></span>|<span data-ttu-id="c2df1-165">Yok</span><span class="sxs-lookup"><span data-stu-id="c2df1-165">N/A</span></span>|  
|<span data-ttu-id="c2df1-166">sunmaya üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="c2df1-166">expose-headers</span></span>|<span data-ttu-id="c2df1-167">Bu öğeyi içeren `header` öğeleri hello istemci tarafından erişilebilecek hello başlıklarının adlarını belirtme.</span><span class="sxs-lookup"><span data-stu-id="c2df1-167">This element contains `header` elements specifying names of hello headers that will be accessible by hello client.</span></span>|<span data-ttu-id="c2df1-168">Hayır</span><span class="sxs-lookup"><span data-stu-id="c2df1-168">No</span></span>|<span data-ttu-id="c2df1-169">Yok</span><span class="sxs-lookup"><span data-stu-id="c2df1-169">N/A</span></span>|  
|<span data-ttu-id="c2df1-170">üst bilgi</span><span class="sxs-lookup"><span data-stu-id="c2df1-170">header</span></span>|<span data-ttu-id="c2df1-171">Bir üstbilgi adı belirtir.</span><span class="sxs-lookup"><span data-stu-id="c2df1-171">Specifies a header name.</span></span>|<span data-ttu-id="c2df1-172">En az bir `header` öğesi gerekli `allowed-headers` veya `expose-headers` hello bölüm mevcut değilse.</span><span class="sxs-lookup"><span data-stu-id="c2df1-172">At least one `header` element is required in `allowed-headers` or `expose-headers` if hello section is present.</span></span>|<span data-ttu-id="c2df1-173">Yok</span><span class="sxs-lookup"><span data-stu-id="c2df1-173">N/A</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="c2df1-174">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="c2df1-174">Attributes</span></span>  
  
|<span data-ttu-id="c2df1-175">Ad</span><span class="sxs-lookup"><span data-stu-id="c2df1-175">Name</span></span>|<span data-ttu-id="c2df1-176">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c2df1-176">Description</span></span>|<span data-ttu-id="c2df1-177">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c2df1-177">Required</span></span>|<span data-ttu-id="c2df1-178">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="c2df1-178">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c2df1-179">izin ver-kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="c2df1-179">allow-credentials</span></span>|<span data-ttu-id="c2df1-180">Merhaba `Access-Control-Allow-Credentials` hello ön yanıt üstbilgisi kümesi toohello değeri bu özniteliğin olmalı ve etki alanları arası istek hello istemcinin özelliği toosubmit kimlik bilgileri etkiler.</span><span class="sxs-lookup"><span data-stu-id="c2df1-180">hello `Access-Control-Allow-Credentials` header in hello preflight response will be set toohello value of this attribute and affect hello client’s ability toosubmit credentials in cross-domain requests.</span></span>|<span data-ttu-id="c2df1-181">Hayır</span><span class="sxs-lookup"><span data-stu-id="c2df1-181">No</span></span>|<span data-ttu-id="c2df1-182">False</span><span class="sxs-lookup"><span data-stu-id="c2df1-182">false</span></span>|  
|<span data-ttu-id="c2df1-183">Ön-sonuç-max-age</span><span class="sxs-lookup"><span data-stu-id="c2df1-183">preflight-result-max-age</span></span>|<span data-ttu-id="c2df1-184">Merhaba `Access-Control-Max-Age` hello ön yanıt üstbilgisi kümesi toohello değeri bu özniteliğin olmalı ve hello kullanıcı aracısının özelliği toocache öncesi uçuş yanıt etkiler.</span><span class="sxs-lookup"><span data-stu-id="c2df1-184">hello `Access-Control-Max-Age` header in hello preflight response will be set toohello value of this attribute and affect hello user agent’s ability toocache pre-flight response.</span></span>|<span data-ttu-id="c2df1-185">Hayır</span><span class="sxs-lookup"><span data-stu-id="c2df1-185">No</span></span>|<span data-ttu-id="c2df1-186">0</span><span class="sxs-lookup"><span data-stu-id="c2df1-186">0</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c2df1-187">Kullanım</span><span class="sxs-lookup"><span data-stu-id="c2df1-187">Usage</span></span>  
 <span data-ttu-id="c2df1-188">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c2df1-188">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c2df1-189">**İlke bölümleri:** gelen</span><span class="sxs-lookup"><span data-stu-id="c2df1-189">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="c2df1-190">**İlke kapsamları:** API, işlemi</span><span class="sxs-lookup"><span data-stu-id="c2df1-190">**Policy scopes:** API, operation</span></span>  
  
##  <span data-ttu-id="c2df1-191"><a name="JSONP"></a>JSONP</span><span class="sxs-lookup"><span data-stu-id="c2df1-191"><a name="JSONP"></a> JSONP</span></span>  
 <span data-ttu-id="c2df1-192">Merhaba `jsonp` İlkesi (JSONP) destek tooan işlem ya da bir API tooallow etki alanları arası çağrılar JavaScript tarayıcı tabanlı istemcilerden doldurma ile JSON ekler.</span><span class="sxs-lookup"><span data-stu-id="c2df1-192">hello `jsonp` policy adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span> <span data-ttu-id="c2df1-193">JSONP JavaScript programları toorequest verileri farklı bir etki alanındaki bir sunucudan kullanılan bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="c2df1-193">JSONP is a method used in JavaScript programs toorequest data from a server in a different domain.</span></span> <span data-ttu-id="c2df1-194">JSONP atlar burada erişim tooweb sayfaları olmalıdır hello çoğu web tarayıcısı tarafından uygulanan hello sınırlaması aynı etki alanı.</span><span class="sxs-lookup"><span data-stu-id="c2df1-194">JSONP bypasses hello limitation enforced by most web browsers where access tooweb pages must be in hello same domain.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c2df1-195">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="c2df1-195">Policy statement</span></span>  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a><span data-ttu-id="c2df1-196">Örnek</span><span class="sxs-lookup"><span data-stu-id="c2df1-196">Example</span></span>  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 <span data-ttu-id="c2df1-197">Merhaba geri çağırma parametresi olmadan hello yöntemini çağırırsanız? cb = XXX (olmadan işlev çağrısı sarmalayıcı) düz JSON döndürecektir.</span><span class="sxs-lookup"><span data-stu-id="c2df1-197">If you call hello method without hello callback parameter ?cb=XXX it will return plain JSON (without a function call wrapper).</span></span>  
  
 <span data-ttu-id="c2df1-198">Merhaba geri çağırma parametresi eklerseniz `?cb=XXX` hello özgün JSON sonuçları gibi hello geri çağırma işlevi geçici kaydırma bir JSONP sonucunu döndürür`XYZ('<json result goes here>');`</span><span class="sxs-lookup"><span data-stu-id="c2df1-198">If you add hello callback parameter `?cb=XXX` it will return a JSONP result, wrapping hello original JSON results around hello callback function like `XYZ('<json result goes here>');`</span></span>  
  
### <a name="elements"></a><span data-ttu-id="c2df1-199">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="c2df1-199">Elements</span></span>  
  
|<span data-ttu-id="c2df1-200">Ad</span><span class="sxs-lookup"><span data-stu-id="c2df1-200">Name</span></span>|<span data-ttu-id="c2df1-201">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c2df1-201">Description</span></span>|<span data-ttu-id="c2df1-202">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c2df1-202">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c2df1-203">jsonp</span><span class="sxs-lookup"><span data-stu-id="c2df1-203">jsonp</span></span>|<span data-ttu-id="c2df1-204">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="c2df1-204">Root element.</span></span>|<span data-ttu-id="c2df1-205">Evet</span><span class="sxs-lookup"><span data-stu-id="c2df1-205">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="c2df1-206">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="c2df1-206">Attributes</span></span>  
  
|<span data-ttu-id="c2df1-207">Ad</span><span class="sxs-lookup"><span data-stu-id="c2df1-207">Name</span></span>|<span data-ttu-id="c2df1-208">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c2df1-208">Description</span></span>|<span data-ttu-id="c2df1-209">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c2df1-209">Required</span></span>|<span data-ttu-id="c2df1-210">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="c2df1-210">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c2df1-211">geri çağırma parametre adı</span><span class="sxs-lookup"><span data-stu-id="c2df1-211">callback-parameter-name</span></span>|<span data-ttu-id="c2df1-212">Merhaba etki alanları arası JavaScript işlev çağrısı hello işlevi bulunduğu hello tam etki alanı adı öneki.</span><span class="sxs-lookup"><span data-stu-id="c2df1-212">hello cross-domain JavaScript function call prefixed with hello fully qualified domain name where hello function resides.</span></span>|<span data-ttu-id="c2df1-213">Evet</span><span class="sxs-lookup"><span data-stu-id="c2df1-213">Yes</span></span>|<span data-ttu-id="c2df1-214">Yok</span><span class="sxs-lookup"><span data-stu-id="c2df1-214">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c2df1-215">Kullanım</span><span class="sxs-lookup"><span data-stu-id="c2df1-215">Usage</span></span>  
 <span data-ttu-id="c2df1-216">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c2df1-216">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c2df1-217">**İlke bölümleri:** giden</span><span class="sxs-lookup"><span data-stu-id="c2df1-217">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="c2df1-218">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="c2df1-218">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="c2df1-219">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c2df1-219">Next steps</span></span>
<span data-ttu-id="c2df1-220">İlkeleriyle çalışma daha fazla bilgi için bkz: [API Management ilkeleri](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="c2df1-220">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  