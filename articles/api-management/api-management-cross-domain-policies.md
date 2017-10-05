---
title: "Azure API Management etki alanları arası ilkeler | Microsoft Docs"
description: "Azure API Management'te kullanıma etki alanları arası ilkeler hakkında bilgi edinin."
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
ms.openlocfilehash: ddca9e35b44a21294abbb5eaa4418bcdb85494cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-cross-domain-policies"></a><span data-ttu-id="8cf4e-103">API Management etki alanları arası ilkeler</span><span class="sxs-lookup"><span data-stu-id="8cf4e-103">API Management cross domain policies</span></span>
<span data-ttu-id="8cf4e-104">Bu konu aşağıdaki API Management ilkeleri bir başvuru sağlar.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="8cf4e-105">Ekleme ve ilkeleri yapılandırma hakkında daha fazla bilgi için bkz: [API Management ilkeleri](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="8cf4e-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="8cf4e-106"><a name="CrossDomainPolicies"></a>Etki alanı ilkelerini arası</span><span class="sxs-lookup"><span data-stu-id="8cf4e-106"><a name="CrossDomainPolicies"></a> Cross domain policies</span></span>  
  
-   <span data-ttu-id="8cf4e-107">[Etki alanları arası çağrılar izin](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -API Adobe Flash ve Microsoft Silverlight tarayıcı tabanlı istemcilerden erişilebilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-107">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
-   <span data-ttu-id="8cf4e-108">[CORS](api-management-cross-domain-policies.md#CORS) -çıkış noktaları arası kaynak paylaşımı (CORS) desteklemek için bir işlem veya tarayıcı tabanlı istemcilerden etki alanları arası çağrılarına izin vermek için bir API ekler.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-108">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
-   <span data-ttu-id="8cf4e-109">[JSONP](api-management-cross-domain-policies.md#JSONP) -bir işlem veya tarayıcı tabanlı JavaScript istemcilerden etki alanları arası çağrılarına izin vermek için bir API (JSONP) doldurma desteğiyle JSON ekler.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
##  <span data-ttu-id="8cf4e-110"><a name="AllowCrossDomainCalls"></a>Etki alanları arası çağrılar izin ver</span><span class="sxs-lookup"><span data-stu-id="8cf4e-110"><a name="AllowCrossDomainCalls"></a> Allow cross-domain calls</span></span>  
 <span data-ttu-id="8cf4e-111">Kullanım `cross-domain` API Adobe Flash ve Microsoft Silverlight tarayıcı tabanlı istemcilerden erişilebilir olması için ilke.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-111">Use the `cross-domain` policy to make the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8cf4e-112">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="8cf4e-112">Policy statement</span></span>  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in the Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a><span data-ttu-id="8cf4e-113">Örnek</span><span class="sxs-lookup"><span data-stu-id="8cf4e-113">Example</span></span>  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a><span data-ttu-id="8cf4e-114">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="8cf4e-114">Elements</span></span>  
  
|<span data-ttu-id="8cf4e-115">Ad</span><span class="sxs-lookup"><span data-stu-id="8cf4e-115">Name</span></span>|<span data-ttu-id="8cf4e-116">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cf4e-116">Description</span></span>|<span data-ttu-id="8cf4e-117">Gerekli</span><span class="sxs-lookup"><span data-stu-id="8cf4e-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="8cf4e-118">etki alanları arası</span><span class="sxs-lookup"><span data-stu-id="8cf4e-118">cross-domain</span></span>|<span data-ttu-id="8cf4e-119">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-119">Root element.</span></span> <span data-ttu-id="8cf4e-120">Alt öğeler için uygun olmalıdır [Adobe etki alanları arası ilke dosya belirtimi](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span><span class="sxs-lookup"><span data-stu-id="8cf4e-120">Child elements must conform to the [Adobe cross-domain policy file specification](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span></span>|<span data-ttu-id="8cf4e-121">Evet</span><span class="sxs-lookup"><span data-stu-id="8cf4e-121">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8cf4e-122">Kullanım</span><span class="sxs-lookup"><span data-stu-id="8cf4e-122">Usage</span></span>  
 <span data-ttu-id="8cf4e-123">Bu ilke aşağıdaki ilkesi kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="8cf4e-123">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8cf4e-124">**İlke bölümleri:** gelen</span><span class="sxs-lookup"><span data-stu-id="8cf4e-124">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="8cf4e-125">**İlke kapsamları:** genel</span><span class="sxs-lookup"><span data-stu-id="8cf4e-125">**Policy scopes:** global</span></span>  
  
##  <span data-ttu-id="8cf4e-126"><a name="CORS"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="8cf4e-126"><a name="CORS"></a> CORS</span></span>  
 <span data-ttu-id="8cf4e-127">`cors` İlkesi çıkış noktaları arası kaynak paylaşımı (CORS) desteklemek için bir işlem veya tarayıcı tabanlı istemcilerden etki alanları arası çağrılarına izin vermek için bir API ekler.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-127">The `cors` policy adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
 <span data-ttu-id="8cf4e-128">CORS bir tarayıcı ile etkileşim kurmanızı ve belirli cross-origin istekleri (JavaScript'ten bir web sayfasında diğer etki alanlarına yapılan yani XMLHttpRequests çağrıları) izin verilip verilmeyeceğini belirlemek için sunucusu sağlar.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-128">CORS allows a browser and a server to interact and determine whether or not to allow specific cross-origin requests (i.e. XMLHttpRequests calls made from JavaScript on a web page to other domains).</span></span> <span data-ttu-id="8cf4e-129">Bu, yalnızca kaynak aynı isteklerine izin'den daha fazla esneklik sağlar, ancak tüm çıkış noktaları arası istekleri izin vererek değerinden daha güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-129">This allows for more flexibility than only allowing same-origin requests, but is more secure than allowing all cross-origin requests.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8cf4e-130">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="8cf4e-130">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="8cf4e-131">Örnek</span><span class="sxs-lookup"><span data-stu-id="8cf4e-131">Example</span></span>  
 <span data-ttu-id="8cf4e-132">Bu örnek özel üstbilgi veya dışında GET ve POST yöntemleri olanlar gibi ön uçuş isteklerini destekleyecek şekilde nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-132">This example demonstrates how to support pre-flight requests, such as those with custom headers or methods other than GET and POST.</span></span> <span data-ttu-id="8cf4e-133">Özel üstbilgi ve ek HTTP fiilleri desteklemek için kullanma `allowed-methods` ve `allowed-headers` bölümler aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-133">To support custom headers and additional HTTP verbs, use the `allowed-methods` and `allowed-headers` sections as shown in the following example.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="8cf4e-134">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="8cf4e-134">Elements</span></span>  
  
|<span data-ttu-id="8cf4e-135">Ad</span><span class="sxs-lookup"><span data-stu-id="8cf4e-135">Name</span></span>|<span data-ttu-id="8cf4e-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cf4e-136">Description</span></span>|<span data-ttu-id="8cf4e-137">Gerekli</span><span class="sxs-lookup"><span data-stu-id="8cf4e-137">Required</span></span>|<span data-ttu-id="8cf4e-138">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="8cf4e-138">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="8cf4e-139">cors</span><span class="sxs-lookup"><span data-stu-id="8cf4e-139">cors</span></span>|<span data-ttu-id="8cf4e-140">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-140">Root element.</span></span>|<span data-ttu-id="8cf4e-141">Evet</span><span class="sxs-lookup"><span data-stu-id="8cf4e-141">Yes</span></span>|<span data-ttu-id="8cf4e-142">Yok</span><span class="sxs-lookup"><span data-stu-id="8cf4e-142">N/A</span></span>|  
|<span data-ttu-id="8cf4e-143">izin verilen çıkış</span><span class="sxs-lookup"><span data-stu-id="8cf4e-143">allowed-origins</span></span>|<span data-ttu-id="8cf4e-144">İçeren `origin` etki alanları arası istekleri için izin verilen çıkış noktası açıklayan öğeler.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-144">Contains `origin` elements that describe the allowed origins for cross-domain requests.</span></span> <span data-ttu-id="8cf4e-145">`allowed-origins`ya da tek bir içerebilir `origin` belirtir öğesi `*` her türlü kaynağa veya bir veya daha fazla izin vermek için `origin` bir URI içeren öğeler.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-145">`allowed-origins` can contain either a single `origin` element that specifies `*` to allow any origin, or one or more `origin` elements that contain a URI.</span></span>|<span data-ttu-id="8cf4e-146">Evet</span><span class="sxs-lookup"><span data-stu-id="8cf4e-146">Yes</span></span>|<span data-ttu-id="8cf4e-147">Yok</span><span class="sxs-lookup"><span data-stu-id="8cf4e-147">N/A</span></span>|  
|<span data-ttu-id="8cf4e-148">Kaynak</span><span class="sxs-lookup"><span data-stu-id="8cf4e-148">origin</span></span>|<span data-ttu-id="8cf4e-149">Değer, ya da olabilir `*` tüm kaynaklara ya da tek bir kaynak belirten bir URI izin vermek için.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-149">The value can be either `*` to allow all origins, or a URI that specifies a single origin.</span></span> <span data-ttu-id="8cf4e-150">URI şeması, ana bilgisayar ve bağlantı noktası eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-150">The URI must include a scheme, host, and port.</span></span>|<span data-ttu-id="8cf4e-151">Evet</span><span class="sxs-lookup"><span data-stu-id="8cf4e-151">Yes</span></span>|<span data-ttu-id="8cf4e-152">Bağlantı noktası bir URI atlanırsa, HTTP için 80 numaralı bağlantı noktası kullanılır ve HTTPS için 443 numaralı bağlantı noktası kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-152">If the port is omitted in a URI, port 80 is used for HTTP and port 443 is used for HTTPS.</span></span>|  
|<span data-ttu-id="8cf4e-153">izin verilen yöntemleri</span><span class="sxs-lookup"><span data-stu-id="8cf4e-153">allowed-methods</span></span>|<span data-ttu-id="8cf4e-154">Yöntemleri dışında GET veya POST izin verilir, bu öğe gereklidir.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-154">This element is required if methods other than GET or POST are allowed.</span></span> <span data-ttu-id="8cf4e-155">İçeren `method` desteklenen HTTP fiilleri öğeleri.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-155">Contains `method` elements that specify the supported HTTP verbs.</span></span>|<span data-ttu-id="8cf4e-156">Hayır</span><span class="sxs-lookup"><span data-stu-id="8cf4e-156">No</span></span>|<span data-ttu-id="8cf4e-157">Bu bölümde mevcut değilse, GET ve POST desteklenir.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-157">If this section is not present, GET and POST are supported.</span></span>|  
|<span data-ttu-id="8cf4e-158">Yöntemi</span><span class="sxs-lookup"><span data-stu-id="8cf4e-158">method</span></span>|<span data-ttu-id="8cf4e-159">Bir HTTP fiili belirtir.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-159">Specifies an HTTP verb.</span></span>|<span data-ttu-id="8cf4e-160">En az bir `method` öğesi, varsa gereklidir `allowed-methods` bölüm mevcut.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-160">At least one `method` element is required if the `allowed-methods` section is present.</span></span>|<span data-ttu-id="8cf4e-161">Yok</span><span class="sxs-lookup"><span data-stu-id="8cf4e-161">N/A</span></span>|  
|<span data-ttu-id="8cf4e-162">izin verilen üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="8cf4e-162">allowed-headers</span></span>|<span data-ttu-id="8cf4e-163">Bu öğeyi içeren `header` öğeleri isteğine dahil başlıklarının adlarını belirtme.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-163">This element contains `header` elements specifying names of the headers that can be included in the request.</span></span>|<span data-ttu-id="8cf4e-164">Hayır</span><span class="sxs-lookup"><span data-stu-id="8cf4e-164">No</span></span>|<span data-ttu-id="8cf4e-165">Yok</span><span class="sxs-lookup"><span data-stu-id="8cf4e-165">N/A</span></span>|  
|<span data-ttu-id="8cf4e-166">sunmaya üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="8cf4e-166">expose-headers</span></span>|<span data-ttu-id="8cf4e-167">Bu öğeyi içeren `header` öğeleri istemci tarafından erişilebilecek başlıklarının adlarını belirtme.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-167">This element contains `header` elements specifying names of the headers that will be accessible by the client.</span></span>|<span data-ttu-id="8cf4e-168">Hayır</span><span class="sxs-lookup"><span data-stu-id="8cf4e-168">No</span></span>|<span data-ttu-id="8cf4e-169">Yok</span><span class="sxs-lookup"><span data-stu-id="8cf4e-169">N/A</span></span>|  
|<span data-ttu-id="8cf4e-170">üst bilgi</span><span class="sxs-lookup"><span data-stu-id="8cf4e-170">header</span></span>|<span data-ttu-id="8cf4e-171">Bir üstbilgi adı belirtir.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-171">Specifies a header name.</span></span>|<span data-ttu-id="8cf4e-172">En az bir `header` öğesi gerekli `allowed-headers` veya `expose-headers` bölüm mevcut değilse.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-172">At least one `header` element is required in `allowed-headers` or `expose-headers` if the section is present.</span></span>|<span data-ttu-id="8cf4e-173">Yok</span><span class="sxs-lookup"><span data-stu-id="8cf4e-173">N/A</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="8cf4e-174">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="8cf4e-174">Attributes</span></span>  
  
|<span data-ttu-id="8cf4e-175">Ad</span><span class="sxs-lookup"><span data-stu-id="8cf4e-175">Name</span></span>|<span data-ttu-id="8cf4e-176">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cf4e-176">Description</span></span>|<span data-ttu-id="8cf4e-177">Gerekli</span><span class="sxs-lookup"><span data-stu-id="8cf4e-177">Required</span></span>|<span data-ttu-id="8cf4e-178">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="8cf4e-178">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="8cf4e-179">izin ver-kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="8cf4e-179">allow-credentials</span></span>|<span data-ttu-id="8cf4e-180">`Access-Control-Allow-Credentials` Ön yanıt üstbilgisi bu özniteliğin değerini ayarlayın ve istemci kimlik bilgileri etki alanları arası istek gönderme olanağı etkiler.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-180">The `Access-Control-Allow-Credentials` header in the preflight response will be set to the value of this attribute and affect the client’s ability to submit credentials in cross-domain requests.</span></span>|<span data-ttu-id="8cf4e-181">Hayır</span><span class="sxs-lookup"><span data-stu-id="8cf4e-181">No</span></span>|<span data-ttu-id="8cf4e-182">False</span><span class="sxs-lookup"><span data-stu-id="8cf4e-182">false</span></span>|  
|<span data-ttu-id="8cf4e-183">Ön-sonuç-max-age</span><span class="sxs-lookup"><span data-stu-id="8cf4e-183">preflight-result-max-age</span></span>|<span data-ttu-id="8cf4e-184">`Access-Control-Max-Age` Ön yanıt üstbilgisi bu özniteliğin değerini ayarlayın ve önbellek öncesi uçuş yanıtı kullanıcı aracısının yeteneği etkiler.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-184">The `Access-Control-Max-Age` header in the preflight response will be set to the value of this attribute and affect the user agent’s ability to cache pre-flight response.</span></span>|<span data-ttu-id="8cf4e-185">Hayır</span><span class="sxs-lookup"><span data-stu-id="8cf4e-185">No</span></span>|<span data-ttu-id="8cf4e-186">0</span><span class="sxs-lookup"><span data-stu-id="8cf4e-186">0</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8cf4e-187">Kullanım</span><span class="sxs-lookup"><span data-stu-id="8cf4e-187">Usage</span></span>  
 <span data-ttu-id="8cf4e-188">Bu ilke aşağıdaki ilkesi kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="8cf4e-188">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8cf4e-189">**İlke bölümleri:** gelen</span><span class="sxs-lookup"><span data-stu-id="8cf4e-189">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="8cf4e-190">**İlke kapsamları:** API, işlemi</span><span class="sxs-lookup"><span data-stu-id="8cf4e-190">**Policy scopes:** API, operation</span></span>  
  
##  <span data-ttu-id="8cf4e-191"><a name="JSONP"></a>JSONP</span><span class="sxs-lookup"><span data-stu-id="8cf4e-191"><a name="JSONP"></a> JSONP</span></span>  
 <span data-ttu-id="8cf4e-192">`jsonp` İlkesi bir işlem veya tarayıcı tabanlı JavaScript istemcilerden etki alanları arası çağrılarına izin vermek için bir API (JSONP) doldurma desteğiyle JSON ekler.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-192">The `jsonp` policy adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span> <span data-ttu-id="8cf4e-193">JSONP JavaScript programlarda farklı bir etki alanındaki bir sunucudan istek verileri için kullanılan bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-193">JSONP is a method used in JavaScript programs to request data from a server in a different domain.</span></span> <span data-ttu-id="8cf4e-194">JSONP burada web sayfalarına erişimi aynı etki alanında olmalıdır çoğu web tarayıcısı tarafından uygulanan sınırlama atlar.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-194">JSONP bypasses the limitation enforced by most web browsers where access to web pages must be in the same domain.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8cf4e-195">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="8cf4e-195">Policy statement</span></span>  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a><span data-ttu-id="8cf4e-196">Örnek</span><span class="sxs-lookup"><span data-stu-id="8cf4e-196">Example</span></span>  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 <span data-ttu-id="8cf4e-197">Geri çağırma parametresi olmadan yöntemini çağırırsanız? cb = XXX (olmadan işlev çağrısı sarmalayıcı) düz JSON döndürecektir.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-197">If you call the method without the callback parameter ?cb=XXX it will return plain JSON (without a function call wrapper).</span></span>  
  
 <span data-ttu-id="8cf4e-198">Geri çağırma parametresi eklerseniz `?cb=XXX` bir JSONP sonuç döndürür ve özgün JSON kaydırma geri çağırma işlevi geçici Sonuçlardan memnun`XYZ('<json result goes here>');`</span><span class="sxs-lookup"><span data-stu-id="8cf4e-198">If you add the callback parameter `?cb=XXX` it will return a JSONP result, wrapping the original JSON results around the callback function like `XYZ('<json result goes here>');`</span></span>  
  
### <a name="elements"></a><span data-ttu-id="8cf4e-199">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="8cf4e-199">Elements</span></span>  
  
|<span data-ttu-id="8cf4e-200">Ad</span><span class="sxs-lookup"><span data-stu-id="8cf4e-200">Name</span></span>|<span data-ttu-id="8cf4e-201">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cf4e-201">Description</span></span>|<span data-ttu-id="8cf4e-202">Gerekli</span><span class="sxs-lookup"><span data-stu-id="8cf4e-202">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="8cf4e-203">jsonp</span><span class="sxs-lookup"><span data-stu-id="8cf4e-203">jsonp</span></span>|<span data-ttu-id="8cf4e-204">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-204">Root element.</span></span>|<span data-ttu-id="8cf4e-205">Evet</span><span class="sxs-lookup"><span data-stu-id="8cf4e-205">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="8cf4e-206">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="8cf4e-206">Attributes</span></span>  
  
|<span data-ttu-id="8cf4e-207">Ad</span><span class="sxs-lookup"><span data-stu-id="8cf4e-207">Name</span></span>|<span data-ttu-id="8cf4e-208">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cf4e-208">Description</span></span>|<span data-ttu-id="8cf4e-209">Gerekli</span><span class="sxs-lookup"><span data-stu-id="8cf4e-209">Required</span></span>|<span data-ttu-id="8cf4e-210">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="8cf4e-210">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="8cf4e-211">geri çağırma parametre adı</span><span class="sxs-lookup"><span data-stu-id="8cf4e-211">callback-parameter-name</span></span>|<span data-ttu-id="8cf4e-212">İşlevin yer tam etki alanı adıyla önek etki alanları arası JavaScript işlevi çağrısı.</span><span class="sxs-lookup"><span data-stu-id="8cf4e-212">The cross-domain JavaScript function call prefixed with the fully qualified domain name where the function resides.</span></span>|<span data-ttu-id="8cf4e-213">Evet</span><span class="sxs-lookup"><span data-stu-id="8cf4e-213">Yes</span></span>|<span data-ttu-id="8cf4e-214">Yok</span><span class="sxs-lookup"><span data-stu-id="8cf4e-214">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8cf4e-215">Kullanım</span><span class="sxs-lookup"><span data-stu-id="8cf4e-215">Usage</span></span>  
 <span data-ttu-id="8cf4e-216">Bu ilke aşağıdaki ilkesi kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="8cf4e-216">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8cf4e-217">**İlke bölümleri:** giden</span><span class="sxs-lookup"><span data-stu-id="8cf4e-217">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="8cf4e-218">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="8cf4e-218">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="8cf4e-219">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8cf4e-219">Next steps</span></span>
<span data-ttu-id="8cf4e-220">İlkeleriyle çalışma daha fazla bilgi için bkz: [API Management ilkeleri](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="8cf4e-220">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  