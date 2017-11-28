---
title: "Azure API Management dönüştürme ilkelerini | Microsoft Docs"
description: "Azure API Management'te kullanıma dönüştürme ilkeleri hakkında bilgi edinin."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7406a8ce-5f9c-4fae-9b0f-e574befb2ee9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: c2bed904b82c569b28a6e00d0cc9b49107c148dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-transformation-policies"></a><span data-ttu-id="578ca-103">API Management dönüştürme ilkelerini</span><span class="sxs-lookup"><span data-stu-id="578ca-103">API Management transformation policies</span></span>
<span data-ttu-id="578ca-104">Bu konu aşağıdaki API Management ilkeleri bir başvuru sağlar.</span><span class="sxs-lookup"><span data-stu-id="578ca-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="578ca-105">Ekleme ve ilkeleri yapılandırma hakkında daha fazla bilgi için bkz: [API Management ilkeleri](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="578ca-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="578ca-106"><a name="TransformationPolicies"></a>Dönüştürme ilkelerini</span><span class="sxs-lookup"><span data-stu-id="578ca-106"><a name="TransformationPolicies"></a> Transformation policies</span></span>  
  
-   <span data-ttu-id="578ca-107">[XML ve JSON Dönüştür](api-management-transformation-policies.md#ConvertJSONtoXML) - dönüştürür isteği veya yanıtı XML ve JSON öğesinden gövde.</span><span class="sxs-lookup"><span data-stu-id="578ca-107">[Convert JSON to XML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON to XML.</span></span>  
  
-   <span data-ttu-id="578ca-108">[XML JSON biçimine Dönüştür](api-management-transformation-policies.md#ConvertXMLtoJSON) - dönüştürür isteği veya yanıtı için JSON XML'den gövde.</span><span class="sxs-lookup"><span data-stu-id="578ca-108">[Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML to JSON.</span></span>  
  
-   <span data-ttu-id="578ca-109">[Bulma ve değiştirme dizesi gövdesi içinde](api-management-transformation-policies.md#Findandreplacestringinbody) - bir istek veya yanıt alt dizeyi bulur ve farklı bir dizeyle değiştirir.</span><span class="sxs-lookup"><span data-stu-id="578ca-109">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
-   <span data-ttu-id="578ca-110">[İçeriği URL'leri maske](api-management-transformation-policies.md#MaskURLSContent) -yanıta bağlantı (maskeleri)'yeniden yazar gövde böylece bunlar ağ geçidi aracılığıyla eşdeğer bağlantı üzerine gelin.</span><span class="sxs-lookup"><span data-stu-id="578ca-110">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span>  
  
-   <span data-ttu-id="578ca-111">[Arka uç hizmetini ayarlamak](api-management-transformation-policies.md#SetBackendService) -gelen bir istek için arka uç hizmeti değiştirir.</span><span class="sxs-lookup"><span data-stu-id="578ca-111">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes the backend service for an incoming request.</span></span>  
  
-   <span data-ttu-id="578ca-112">[Gövde ayarlamak](api-management-transformation-policies.md#SetBody) -ileti gövdesi gelen ve giden istekleri için ayarlar.</span><span class="sxs-lookup"><span data-stu-id="578ca-112">[Set body](api-management-transformation-policies.md#SetBody) - Sets the message body for incoming and outgoing requests.</span></span>  
  
-   <span data-ttu-id="578ca-113">[HTTP üstbilgisi kümesi](api-management-transformation-policies.md#SetHTTPheader) - değer atayan bir varolan yanıt ve/veya istek üstbilgisi veya yeni bir yanıt ve/veya istek üstbilgisi ekler.</span><span class="sxs-lookup"><span data-stu-id="578ca-113">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
-   <span data-ttu-id="578ca-114">[Sorgu dizesi parametresi kümesi](api-management-transformation-policies.md#SetQueryStringParameter) - ekler, değiştirir değerini veya istek sorgu dizesi parametresi siler.</span><span class="sxs-lookup"><span data-stu-id="578ca-114">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
-   <span data-ttu-id="578ca-115">[URL yeniden yazma](api-management-transformation-policies.md#RewriteURL) -bir istek URL'sini ortak formundan web hizmeti tarafından beklenen biçime dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="578ca-115">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form to the form expected by the web service.</span></span>  
  
-   <span data-ttu-id="578ca-116">[XSLT kullanarak XML dönüştürme](api-management-transformation-policies.md#XSLTransform) -XSL dönüşümü istek veya yanıt gövdesinde XML için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="578ca-116">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation to XML in the request or response body.</span></span>  
  
##  <span data-ttu-id="578ca-117"><a name="ConvertJSONtoXML"></a>XML ve JSON Dönüştür</span><span class="sxs-lookup"><span data-stu-id="578ca-117"><a name="ConvertJSONtoXML"></a> Convert JSON to XML</span></span>  
 <span data-ttu-id="578ca-118">`json-to-xml` İlkesi JSON öğesinden bir istek veya yanıt gövdesi XML'e dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="578ca-118">The `json-to-xml` policy converts a request or response body from JSON to XML.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="578ca-119">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="578ca-119">Policy statement</span></span>  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="578ca-120">Örnek</span><span class="sxs-lookup"><span data-stu-id="578ca-120">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <json-to-xml apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="578ca-121">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="578ca-121">Elements</span></span>  
  
|<span data-ttu-id="578ca-122">Ad</span><span class="sxs-lookup"><span data-stu-id="578ca-122">Name</span></span>|<span data-ttu-id="578ca-123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="578ca-123">Description</span></span>|<span data-ttu-id="578ca-124">Gerekli</span><span class="sxs-lookup"><span data-stu-id="578ca-124">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="578ca-125">JSON xml</span><span class="sxs-lookup"><span data-stu-id="578ca-125">json-to-xml</span></span>|<span data-ttu-id="578ca-126">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="578ca-126">Root element.</span></span>|<span data-ttu-id="578ca-127">Evet</span><span class="sxs-lookup"><span data-stu-id="578ca-127">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="578ca-128">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="578ca-128">Attributes</span></span>  
  
|<span data-ttu-id="578ca-129">Ad</span><span class="sxs-lookup"><span data-stu-id="578ca-129">Name</span></span>|<span data-ttu-id="578ca-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="578ca-130">Description</span></span>|<span data-ttu-id="578ca-131">Gerekli</span><span class="sxs-lookup"><span data-stu-id="578ca-131">Required</span></span>|<span data-ttu-id="578ca-132">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="578ca-132">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="578ca-133">Uygula</span><span class="sxs-lookup"><span data-stu-id="578ca-133">apply</span></span>|<span data-ttu-id="578ca-134">Özniteliği aşağıdaki değerlerden birine ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="578ca-134">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="578ca-135">-her zaman - her zaman dönüştürme uygulanır.</span><span class="sxs-lookup"><span data-stu-id="578ca-135">-   always - always apply conversion.</span></span><br /><span data-ttu-id="578ca-136">Yalnızca yanıt Content-Type üstbilgisi JSON varlığını gösteriyorsa - içerik türü json - dönüştürülemiyor.</span><span class="sxs-lookup"><span data-stu-id="578ca-136">-   content-type-json - convert only if response Content-Type header indicates presence of JSON.</span></span>|<span data-ttu-id="578ca-137">Evet</span><span class="sxs-lookup"><span data-stu-id="578ca-137">Yes</span></span>|<span data-ttu-id="578ca-138">Yok</span><span class="sxs-lookup"><span data-stu-id="578ca-138">N/A</span></span>|  
|<span data-ttu-id="578ca-139">göz önünde bulundurun kabul-üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="578ca-139">consider-accept-header</span></span>|<span data-ttu-id="578ca-140">Özniteliği aşağıdaki değerlerden birine ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="578ca-140">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="578ca-141">JSON istek Accept üstbilgisi isteniyorsa - true - dönüştürme uygulanır.</span><span class="sxs-lookup"><span data-stu-id="578ca-141">-   true - apply conversion if JSON is requested in request Accept header.</span></span><br /><span data-ttu-id="578ca-142">-false - her zaman dönüştürme uygulayın.</span><span class="sxs-lookup"><span data-stu-id="578ca-142">-   false -always apply conversion.</span></span>|<span data-ttu-id="578ca-143">Hayır</span><span class="sxs-lookup"><span data-stu-id="578ca-143">No</span></span>|<span data-ttu-id="578ca-144">TRUE</span><span class="sxs-lookup"><span data-stu-id="578ca-144">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="578ca-145">Kullanım</span><span class="sxs-lookup"><span data-stu-id="578ca-145">Usage</span></span>  
 <span data-ttu-id="578ca-146">Bu ilke aşağıdaki ilkesi kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="578ca-146">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="578ca-147">**İlke bölümleri:** gelen, giden, hata</span><span class="sxs-lookup"><span data-stu-id="578ca-147">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="578ca-148">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="578ca-148">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="578ca-149"><a name="ConvertXMLtoJSON"></a>XML JSON biçimine Dönüştür</span><span class="sxs-lookup"><span data-stu-id="578ca-149"><a name="ConvertXMLtoJSON"></a> Convert XML to JSON</span></span>  
 <span data-ttu-id="578ca-150">`xml-to-json` İlkesi XML'den bir istek veya yanıt gövdesi JSON değerine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="578ca-150">The `xml-to-json` policy converts a request or response body from XML to JSON.</span></span> <span data-ttu-id="578ca-151">Bu ilke, yalnızca XML arka uç web hizmetlerini temel alarak API'leri modernize için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="578ca-151">This policy can be used to modernize APIs based on XML-only backend web services.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="578ca-152">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="578ca-152">Policy statement</span></span>  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="578ca-153">Örnek</span><span class="sxs-lookup"><span data-stu-id="578ca-153">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <xml-to-json kind="direct" apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="578ca-154">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="578ca-154">Elements</span></span>  
  
|<span data-ttu-id="578ca-155">Ad</span><span class="sxs-lookup"><span data-stu-id="578ca-155">Name</span></span>|<span data-ttu-id="578ca-156">Açıklama</span><span class="sxs-lookup"><span data-stu-id="578ca-156">Description</span></span>|<span data-ttu-id="578ca-157">Gerekli</span><span class="sxs-lookup"><span data-stu-id="578ca-157">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="578ca-158">XML json</span><span class="sxs-lookup"><span data-stu-id="578ca-158">xml-to-json</span></span>|<span data-ttu-id="578ca-159">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="578ca-159">Root element.</span></span>|<span data-ttu-id="578ca-160">Evet</span><span class="sxs-lookup"><span data-stu-id="578ca-160">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="578ca-161">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="578ca-161">Attributes</span></span>  
  
|<span data-ttu-id="578ca-162">Ad</span><span class="sxs-lookup"><span data-stu-id="578ca-162">Name</span></span>|<span data-ttu-id="578ca-163">Açıklama</span><span class="sxs-lookup"><span data-stu-id="578ca-163">Description</span></span>|<span data-ttu-id="578ca-164">Gerekli</span><span class="sxs-lookup"><span data-stu-id="578ca-164">Required</span></span>|<span data-ttu-id="578ca-165">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="578ca-165">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="578ca-166">türü</span><span class="sxs-lookup"><span data-stu-id="578ca-166">kind</span></span>|<span data-ttu-id="578ca-167">Özniteliği aşağıdaki değerlerden birine ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="578ca-167">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="578ca-168">javascript-kolay - dönüştürülen JSON JavaScript geliştiricileri için kolay bir form sahiptir.</span><span class="sxs-lookup"><span data-stu-id="578ca-168">-   javascript-friendly - the converted JSON has a form friendly to JavaScript developers.</span></span><br /><span data-ttu-id="578ca-169">-doğrudan - dönüştürülen JSON özgün XML belge yapısını yansıtır.</span><span class="sxs-lookup"><span data-stu-id="578ca-169">-   direct - the converted JSON reflects the original XML document's structure.</span></span>|<span data-ttu-id="578ca-170">Evet</span><span class="sxs-lookup"><span data-stu-id="578ca-170">Yes</span></span>|<span data-ttu-id="578ca-171">Yok</span><span class="sxs-lookup"><span data-stu-id="578ca-171">N/A</span></span>|  
|<span data-ttu-id="578ca-172">Uygula</span><span class="sxs-lookup"><span data-stu-id="578ca-172">apply</span></span>|<span data-ttu-id="578ca-173">Özniteliği aşağıdaki değerlerden birine ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="578ca-173">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="578ca-174">-her zaman - her zaman dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="578ca-174">-   always - convert always.</span></span><br /><span data-ttu-id="578ca-175">Yalnızca yanıt Content-Type üstbilgisi XML varlığını gösteriyorsa - içerik türü xml - dönüştürülemiyor.</span><span class="sxs-lookup"><span data-stu-id="578ca-175">-   content-type-xml - convert only if response Content-Type header indicates presence of XML.</span></span>|<span data-ttu-id="578ca-176">Evet</span><span class="sxs-lookup"><span data-stu-id="578ca-176">Yes</span></span>|<span data-ttu-id="578ca-177">Yok</span><span class="sxs-lookup"><span data-stu-id="578ca-177">N/A</span></span>|  
|<span data-ttu-id="578ca-178">göz önünde bulundurun kabul-üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="578ca-178">consider-accept-header</span></span>|<span data-ttu-id="578ca-179">Özniteliği aşağıdaki değerlerden birine ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="578ca-179">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="578ca-180">XML isteği Accept üstbilgisi isteniyorsa - true - dönüştürme uygulanır.</span><span class="sxs-lookup"><span data-stu-id="578ca-180">-   true - apply conversion if XML is requested in request Accept header.</span></span><br /><span data-ttu-id="578ca-181">-false - her zaman dönüştürme uygulayın.</span><span class="sxs-lookup"><span data-stu-id="578ca-181">-   false -always apply conversion.</span></span>|<span data-ttu-id="578ca-182">Hayır</span><span class="sxs-lookup"><span data-stu-id="578ca-182">No</span></span>|<span data-ttu-id="578ca-183">TRUE</span><span class="sxs-lookup"><span data-stu-id="578ca-183">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="578ca-184">Kullanım</span><span class="sxs-lookup"><span data-stu-id="578ca-184">Usage</span></span>  
 <span data-ttu-id="578ca-185">Bu ilke aşağıdaki ilkesi kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="578ca-185">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="578ca-186">**İlke bölümleri:** gelen, giden, hata</span><span class="sxs-lookup"><span data-stu-id="578ca-186">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="578ca-187">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="578ca-187">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="578ca-188"><a name="Findandreplacestringinbody"></a>Bulma ve gövde dizesinde değiştirme</span><span class="sxs-lookup"><span data-stu-id="578ca-188"><a name="Findandreplacestringinbody"></a> Find and replace string in body</span></span>  
 <span data-ttu-id="578ca-189">`find-and-replace` İlke isteği veya yanıtı alt dizeyi bulur ve farklı bir dizeyle değiştirir.</span><span class="sxs-lookup"><span data-stu-id="578ca-189">The `find-and-replace` policy finds a request or response substring and replaces it with a different substring.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="578ca-190">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="578ca-190">Policy statement</span></span>  
  
```xml  
<find-and-replace from="what to replace" to="replacement" />  
```  
  
### <a name="example"></a><span data-ttu-id="578ca-191">Örnek</span><span class="sxs-lookup"><span data-stu-id="578ca-191">Example</span></span>  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a><span data-ttu-id="578ca-192">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="578ca-192">Elements</span></span>  
  
|<span data-ttu-id="578ca-193">Ad</span><span class="sxs-lookup"><span data-stu-id="578ca-193">Name</span></span>|<span data-ttu-id="578ca-194">Açıklama</span><span class="sxs-lookup"><span data-stu-id="578ca-194">Description</span></span>|<span data-ttu-id="578ca-195">Gerekli</span><span class="sxs-lookup"><span data-stu-id="578ca-195">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="578ca-196">Bul ve Değiştir</span><span class="sxs-lookup"><span data-stu-id="578ca-196">find-and-replace</span></span>|<span data-ttu-id="578ca-197">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="578ca-197">Root element.</span></span>|<span data-ttu-id="578ca-198">Evet</span><span class="sxs-lookup"><span data-stu-id="578ca-198">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="578ca-199">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="578ca-199">Attributes</span></span>  
  
|<span data-ttu-id="578ca-200">Ad</span><span class="sxs-lookup"><span data-stu-id="578ca-200">Name</span></span>|<span data-ttu-id="578ca-201">Açıklama</span><span class="sxs-lookup"><span data-stu-id="578ca-201">Description</span></span>|<span data-ttu-id="578ca-202">Gerekli</span><span class="sxs-lookup"><span data-stu-id="578ca-202">Required</span></span>|<span data-ttu-id="578ca-203">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="578ca-203">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="578ca-204">Kaynak</span><span class="sxs-lookup"><span data-stu-id="578ca-204">from</span></span>|<span data-ttu-id="578ca-205">Aranacak dize.</span><span class="sxs-lookup"><span data-stu-id="578ca-205">The string to search for.</span></span>|<span data-ttu-id="578ca-206">Evet</span><span class="sxs-lookup"><span data-stu-id="578ca-206">Yes</span></span>|<span data-ttu-id="578ca-207">Yok</span><span class="sxs-lookup"><span data-stu-id="578ca-207">N/A</span></span>|  
|<span data-ttu-id="578ca-208">-</span><span class="sxs-lookup"><span data-stu-id="578ca-208">to</span></span>|<span data-ttu-id="578ca-209">Değiştirme dizesi.</span><span class="sxs-lookup"><span data-stu-id="578ca-209">The replacement string.</span></span> <span data-ttu-id="578ca-210">Arama dizesi kaldırmak için bir sıfır uzunluk değiştirme dizesini belirtin.</span><span class="sxs-lookup"><span data-stu-id="578ca-210">Specify a zero length replacement string to remove the search string.</span></span>|<span data-ttu-id="578ca-211">Evet</span><span class="sxs-lookup"><span data-stu-id="578ca-211">Yes</span></span>|<span data-ttu-id="578ca-212">Yok</span><span class="sxs-lookup"><span data-stu-id="578ca-212">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="578ca-213">Kullanım</span><span class="sxs-lookup"><span data-stu-id="578ca-213">Usage</span></span>  
 <span data-ttu-id="578ca-214">Bu ilke aşağıdaki ilkesi kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="578ca-214">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="578ca-215">**İlke bölümleri:** gelen, giden arka uç, hata</span><span class="sxs-lookup"><span data-stu-id="578ca-215">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="578ca-216">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="578ca-216">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="578ca-217"><a name="MaskURLSContent"></a>İçerik maskesi URL'leri</span><span class="sxs-lookup"><span data-stu-id="578ca-217"><a name="MaskURLSContent"></a> Mask URLs in content</span></span>  
 <span data-ttu-id="578ca-218">`redirect-content-urls` İlkesi böylece bunlar ağ geçidi aracılığıyla eşdeğer bağlantı noktası yanıt gövdesi (maskeleri) bağlantıları yeniden yazar.</span><span class="sxs-lookup"><span data-stu-id="578ca-218">The `redirect-content-urls` policy re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span> <span data-ttu-id="578ca-219">Giden bölümünde yanıt gövdesi bağlantılar için ağ geçidi'nin üzerine olmalarını yeniden yazmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="578ca-219">Use in the outbound section to re-write response body links to make them point to the gateway.</span></span> <span data-ttu-id="578ca-220">Gelen bölümünde ters efekt için kullanın.</span><span class="sxs-lookup"><span data-stu-id="578ca-220">Use in the inbound section for an opposite effect.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="578ca-221">Bu ilke tüm üstbilgi değerleri gibi değiştirmez `Location` üstbilgileri.</span><span class="sxs-lookup"><span data-stu-id="578ca-221">This policy does not change any header values such as `Location` headers.</span></span> <span data-ttu-id="578ca-222">Üstbilgi değerlerini değiştirmek için kullanın [set üstbilgisi](api-management-transformation-policies.md#SetHTTPheader) ilkesi.</span><span class="sxs-lookup"><span data-stu-id="578ca-222">To change header values, use the [set-header](api-management-transformation-policies.md#SetHTTPheader) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="578ca-223">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="578ca-223">Policy statement</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a><span data-ttu-id="578ca-224">Örnek</span><span class="sxs-lookup"><span data-stu-id="578ca-224">Example</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a><span data-ttu-id="578ca-225">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="578ca-225">Elements</span></span>  
  
|<span data-ttu-id="578ca-226">Ad</span><span class="sxs-lookup"><span data-stu-id="578ca-226">Name</span></span>|<span data-ttu-id="578ca-227">Açıklama</span><span class="sxs-lookup"><span data-stu-id="578ca-227">Description</span></span>|<span data-ttu-id="578ca-228">Gerekli</span><span class="sxs-lookup"><span data-stu-id="578ca-228">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="578ca-229">Yönlendirme içerik URL'leri</span><span class="sxs-lookup"><span data-stu-id="578ca-229">redirect-content-urls</span></span>|<span data-ttu-id="578ca-230">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="578ca-230">Root element.</span></span>|<span data-ttu-id="578ca-231">Evet</span><span class="sxs-lookup"><span data-stu-id="578ca-231">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="578ca-232">Kullanım</span><span class="sxs-lookup"><span data-stu-id="578ca-232">Usage</span></span>  
 <span data-ttu-id="578ca-233">Bu ilke aşağıdaki ilkesi kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="578ca-233">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="578ca-234">**İlke bölümleri:** gelen, giden</span><span class="sxs-lookup"><span data-stu-id="578ca-234">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="578ca-235">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="578ca-235">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="578ca-236"><a name="SetBackendService"></a>Arka uç hizmet belirleme</span><span class="sxs-lookup"><span data-stu-id="578ca-236"><a name="SetBackendService"></a> Set backend service</span></span>  
 <span data-ttu-id="578ca-237">Kullanım `set-backend-service` gelen bir istek bu işlem için API ayarlarında belirtilenden farklı bir arka uç yeniden yönlendirmek için ilke.</span><span class="sxs-lookup"><span data-stu-id="578ca-237">Use the `set-backend-service` policy to redirect an incoming request to a different backend than the one specified in the API settings for that operation.</span></span> <span data-ttu-id="578ca-238">Bu ilke, ilkede belirtilen karmayla gelen isteği arka uç hizmeti temel URL'sini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="578ca-238">This policy changes the backend service base URL of the incoming request to the one specified in the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="578ca-239">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="578ca-239">Policy statement</span></span>  
  
```xml  
<set-backend-service base-url="base URL of the backend service" />  
```  
  
### <a name="example"></a><span data-ttu-id="578ca-240">Örnek</span><span class="sxs-lookup"><span data-stu-id="578ca-240">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <choose>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2013-05")">  
                <set-backend-service base-url="http://contoso.com/api/8.2/" />  
            </when>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2014-03")">  
                <set-backend-service base-url="http://contoso.com/api/9.1/" />  
            </when>  
        </choose>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
<span data-ttu-id="578ca-241">Bu örnekte, farklı arka uç hizmetine bir API çağrısında belirtilen sorgu dizesinde geçirilen sürüm değere göre isteklerini kümesi arka uç hizmet ilkesi yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="578ca-241">In this example the set backend service policy routes requests based on the version value passed in the query string to a different backend service than the one specified in the API.</span></span>
  
<span data-ttu-id="578ca-242">Başlangıçta arka uç hizmeti temel URL API ayarlarından türetilir.</span><span class="sxs-lookup"><span data-stu-id="578ca-242">Initially the backend service base URL is derived from the API settings.</span></span> <span data-ttu-id="578ca-243">Bu nedenle istek URL'si `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` hale `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` burada `http://contoso.com/api/10.4/` API ayarlarında belirtilen arka uç hizmeti URL.</span><span class="sxs-lookup"><span data-stu-id="578ca-243">So the request URL `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` becomes `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` where `http://contoso.com/api/10.4/` is the backend service URL specified in the API settings.</span></span>  
  
<span data-ttu-id="578ca-244">Zaman [< seçin\> ](api-management-advanced-policies.md#choose) ilke bildirimi uygulanır arka uç hizmeti temel URL ya da yeniden değişebilir `http://contoso.com/api/8.2` veya `http://contoso.com/api/9.1`sürüm istek sorgu parametresinin değeri bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="578ca-244">When the [<choose\>](api-management-advanced-policies.md#choose) policy statement is applied the backend service base URL may change again either to `http://contoso.com/api/8.2` or `http://contoso.com/api/9.1`, depending on the value of the version request query parameter.</span></span> <span data-ttu-id="578ca-245">Örneğin, değer ise `"2013-15"` URL hale son isteği `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span><span class="sxs-lookup"><span data-stu-id="578ca-245">For example, if the value is `"2013-15"` the final request URL becomes `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span></span>  
  
<span data-ttu-id="578ca-246">Daha fazla dönüştürme isteği olup olmadığını istenen, diğer [dönüştürme ilkelerini](api-management-transformation-policies.md#TransformationPolicies) kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="578ca-246">If further transformation of the request is desired, other [Transformation policies](api-management-transformation-policies.md#TransformationPolicies) can be used.</span></span> <span data-ttu-id="578ca-247">Örneğin, istek sürüm belirli arka ucuna yönlendirilen artık version sorgu parametresi kaldırmak için [ayarlamak sorgu dizesi parametresi](api-management-transformation-policies.md#SetQueryStringParameter) İlkesi, şimdi yedek sürüm özniteliğini kaldırmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="578ca-247">For example, to remove the version query parameter now that the request is being routed to a version specific backend, the  [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policy can be used to remove the now redundant version attribute.</span></span>  
  
### <a name="example"></a><span data-ttu-id="578ca-248">Örnek</span><span class="sxs-lookup"><span data-stu-id="578ca-248">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <set-backend-service backend-id="my-sf-service" sf-partition-key="@(context.Request.Url.Query.GetValueOrDefault("userId","")" sf-replica-type="primary" /> 
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
<span data-ttu-id="578ca-249">Bu örnekte, bölüm anahtarı olarak UserID sorgu dizesi kullanılarak ve birincil çoğaltmasını kullanarak bir service fabric arka ucuna, isteği ilkesi yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="578ca-249">In this example the policy routes the request to a service fabric backend, using the userId query string as the partition key and using the primary replica of the partition.</span></span>  

### <a name="elements"></a><span data-ttu-id="578ca-250">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="578ca-250">Elements</span></span>  
  
|<span data-ttu-id="578ca-251">Ad</span><span class="sxs-lookup"><span data-stu-id="578ca-251">Name</span></span>|<span data-ttu-id="578ca-252">Açıklama</span><span class="sxs-lookup"><span data-stu-id="578ca-252">Description</span></span>|<span data-ttu-id="578ca-253">Gerekli</span><span class="sxs-lookup"><span data-stu-id="578ca-253">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="578ca-254">arka uç hizmet belirleme</span><span class="sxs-lookup"><span data-stu-id="578ca-254">set-backend-service</span></span>|<span data-ttu-id="578ca-255">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="578ca-255">Root element.</span></span>|<span data-ttu-id="578ca-256">Evet</span><span class="sxs-lookup"><span data-stu-id="578ca-256">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="578ca-257">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="578ca-257">Attributes</span></span>  
  
|<span data-ttu-id="578ca-258">Ad</span><span class="sxs-lookup"><span data-stu-id="578ca-258">Name</span></span>|<span data-ttu-id="578ca-259">Açıklama</span><span class="sxs-lookup"><span data-stu-id="578ca-259">Description</span></span>|<span data-ttu-id="578ca-260">Gerekli</span><span class="sxs-lookup"><span data-stu-id="578ca-260">Required</span></span>|<span data-ttu-id="578ca-261">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="578ca-261">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="578ca-262">Taban URL'si</span><span class="sxs-lookup"><span data-stu-id="578ca-262">base-url</span></span>|<span data-ttu-id="578ca-263">Yeni arka uç hizmeti temel URL'si.</span><span class="sxs-lookup"><span data-stu-id="578ca-263">New backend service base URL.</span></span>|<span data-ttu-id="578ca-264">Hayır</span><span class="sxs-lookup"><span data-stu-id="578ca-264">No</span></span>|<span data-ttu-id="578ca-265">Yok</span><span class="sxs-lookup"><span data-stu-id="578ca-265">N/A</span></span>|  
|<span data-ttu-id="578ca-266">arka uç kimliği</span><span class="sxs-lookup"><span data-stu-id="578ca-266">backend-id</span></span>|<span data-ttu-id="578ca-267">Yönlendirmek için arka uç tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="578ca-267">Identifier of the backend to route to.</span></span>|<span data-ttu-id="578ca-268">Hayır</span><span class="sxs-lookup"><span data-stu-id="578ca-268">No</span></span>|<span data-ttu-id="578ca-269">Yok</span><span class="sxs-lookup"><span data-stu-id="578ca-269">N/A</span></span>|  
|<span data-ttu-id="578ca-270">BT bölüm anahtarı</span><span class="sxs-lookup"><span data-stu-id="578ca-270">sf-partition-key</span></span>|<span data-ttu-id="578ca-271">Yalnızca arka uç Service Fabric hizmeti ve 'arka uç-ID' kullanılarak belirtilen olduğunda geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="578ca-271">Only applicable when the backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="578ca-272">Belirli bir ad çözümleme hizmeti bölümünden çözmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="578ca-272">Used to resolve a specific partition from the name resolution service.</span></span>|<span data-ttu-id="578ca-273">Hayır</span><span class="sxs-lookup"><span data-stu-id="578ca-273">No</span></span>|<span data-ttu-id="578ca-274">Yok</span><span class="sxs-lookup"><span data-stu-id="578ca-274">N/A</span></span>|  
|<span data-ttu-id="578ca-275">BT çoğaltma türü</span><span class="sxs-lookup"><span data-stu-id="578ca-275">sf-replica-type</span></span>|<span data-ttu-id="578ca-276">Yalnızca arka uç Service Fabric hizmeti ve 'arka uç-ID' kullanılarak belirtilen olduğunda geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="578ca-276">Only applicable when the backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="578ca-277">İstek bir bölüm birincil veya ikincil çoğaltmasının görünmeliyse denetler.</span><span class="sxs-lookup"><span data-stu-id="578ca-277">Controls if the request should go to the primary or secondary replica of a partition.</span></span> |<span data-ttu-id="578ca-278">Hayır</span><span class="sxs-lookup"><span data-stu-id="578ca-278">No</span></span>|<span data-ttu-id="578ca-279">Yok</span><span class="sxs-lookup"><span data-stu-id="578ca-279">N/A</span></span>|    
|<span data-ttu-id="578ca-280">BT çözümleme durumu</span><span class="sxs-lookup"><span data-stu-id="578ca-280">sf-resolve-condition</span></span>|<span data-ttu-id="578ca-281">Yalnızca arka uç Service Fabric hizmeti olduğunda geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="578ca-281">Only applicable when the backend is a Service Fabric service.</span></span> <span data-ttu-id="578ca-282">Service Fabric arka uç çağrısı ile yeni çözünürlüğü yinelenmesini varsa tanımlama koşulu.</span><span class="sxs-lookup"><span data-stu-id="578ca-282">Condition identifying if the call to Service Fabric backend has to be repeated with new resolution.</span></span>|<span data-ttu-id="578ca-283">Hayır</span><span class="sxs-lookup"><span data-stu-id="578ca-283">No</span></span>|<span data-ttu-id="578ca-284">Yok</span><span class="sxs-lookup"><span data-stu-id="578ca-284">N/A</span></span>|    
|<span data-ttu-id="578ca-285">BT hizmet örneği adı</span><span class="sxs-lookup"><span data-stu-id="578ca-285">sf-service-instance-name</span></span>|<span data-ttu-id="578ca-286">Yalnızca arka uç Service Fabric hizmeti olduğunda geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="578ca-286">Only applicable when the backend is a Service Fabric service.</span></span> <span data-ttu-id="578ca-287">Hizmet örnekleri çalışma zamanında değiştirmesine olanak verir.</span><span class="sxs-lookup"><span data-stu-id="578ca-287">Allows to change service instances at runtime.</span></span> |<span data-ttu-id="578ca-288">Hayır</span><span class="sxs-lookup"><span data-stu-id="578ca-288">No</span></span>|<span data-ttu-id="578ca-289">Yok</span><span class="sxs-lookup"><span data-stu-id="578ca-289">N/A</span></span>|    

### <a name="usage"></a><span data-ttu-id="578ca-290">Kullanım</span><span class="sxs-lookup"><span data-stu-id="578ca-290">Usage</span></span>  
 <span data-ttu-id="578ca-291">Bu ilke aşağıdaki ilkesi kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="578ca-291">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="578ca-292">**İlke bölümleri:** gelen, arka uç</span><span class="sxs-lookup"><span data-stu-id="578ca-292">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="578ca-293">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="578ca-293">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="578ca-294"><a name="SetBody"></a>Set gövdesi</span><span class="sxs-lookup"><span data-stu-id="578ca-294"><a name="SetBody"></a> Set body</span></span>  
 <span data-ttu-id="578ca-295">Kullanım `set-body` gelen ve giden istekleri için ileti gövdesi ayarlamak için ilke.</span><span class="sxs-lookup"><span data-stu-id="578ca-295">Use the `set-body` policy to set the message body for incoming and outgoing requests.</span></span> <span data-ttu-id="578ca-296">Kullanabileceğiniz ileti gövdesi erişmek için `context.Request.Body` özelliği veya `context.Response.Body`ilkesi gelen veya giden bölümünde olmasına bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="578ca-296">To access the message body you can use the `context.Request.Body` property or the `context.Response.Body`, depending on whether the policy is in the inbound or outbound section.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="578ca-297">Varsayılan olarak, ileti eriştiğinizde kullanarak gövde unutmayın `context.Request.Body` veya `context.Response.Body`, özgün ileti gövdesi kaybolur ve geri ifadesinde gövdesi döndürerek ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="578ca-297">Note that by default when you access the message body using `context.Request.Body` or `context.Response.Body`, the original message body is lost and must be set by returning the body back in the expression.</span></span> <span data-ttu-id="578ca-298">Gövde içeriği korumak üzere ayarlanmış `preserveContent` parametresi `true` ileti erişirken.</span><span class="sxs-lookup"><span data-stu-id="578ca-298">To preserve the body content, set the `preserveContent` parameter to `true` when accessing the message.</span></span> <span data-ttu-id="578ca-299">Varsa `preserveContent` ayarlanır `true` ve döndürülen gövde kullanılır farklı gövde ifade tarafından döndürülür.</span><span class="sxs-lookup"><span data-stu-id="578ca-299">If `preserveContent` is set to `true` and a different body is returned by the expression, the returned body is used.</span></span>  
>   
>  <span data-ttu-id="578ca-300">Lütfen kullanırken aşağıdaki noktaları unutmayın `set-body` ilkesi.</span><span class="sxs-lookup"><span data-stu-id="578ca-300">Please note the following considerations when using the `set-body` policy.</span></span>  
>   
>  -   <span data-ttu-id="578ca-301">Kullanıyorsanız `set-body` ayarlamak gerekmez yeni veya güncelleştirilmiş bir gövde döndürmek için ilke `preserveContent` için `true` olduğundan yeni gövdesi içeriği açıkça sağlamış olursunuz.</span><span class="sxs-lookup"><span data-stu-id="578ca-301">If you are using the `set-body` policy to return a new or updated body you don't need to set `preserveContent` to `true` because you are explicitly supplying the new body contents.</span></span>  
> -   <span data-ttu-id="578ca-302">Gelen ardışık düzeninde bir yanıt içeriği koruma, olmadığından yanıt henüz doesn't make Sense.</span><span class="sxs-lookup"><span data-stu-id="578ca-302">Preserving the content of a response in the inbound pipeline doesn't make sense because there is no response yet.</span></span>  
> -   <span data-ttu-id="578ca-303">Giden ardışık düzeninde bir isteğin içerik koruma, çünkü istek zaten arka ucuna bu noktada gönderildi doesn't make Sense.</span><span class="sxs-lookup"><span data-stu-id="578ca-303">Preserving the content of a request in the outbound pipeline doesn't make sense because the request has already been sent to the backend at this point.</span></span>  
> -   <span data-ttu-id="578ca-304">Örneğin ileti gövdesi yok olduğunda bu ilkeyi kullandıysanız, gelen bir GET içinde bir özel durum oluşur.</span><span class="sxs-lookup"><span data-stu-id="578ca-304">If this policy is used when there is no message body, for example in an inbound GET, an exception is thrown.</span></span>  
  
 <span data-ttu-id="578ca-305">Daha fazla bilgi için bkz: `context.Request.Body`, `context.Response.Body`ve `IMessage` bölümler [bağlamının](api-management-policy-expressions.md#ContextVariables) tablo.</span><span class="sxs-lookup"><span data-stu-id="578ca-305">For more information, see the `context.Request.Body`, `context.Response.Body`, and the `IMessage` sections in the [Context variable](api-management-policy-expressions.md#ContextVariables) table.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="578ca-306">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="578ca-306">Policy statement</span></span>  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a><span data-ttu-id="578ca-307">Örnekler</span><span class="sxs-lookup"><span data-stu-id="578ca-307">Examples</span></span>  
  
#### <a name="literal-text-example"></a><span data-ttu-id="578ca-308">Değişmez değer metni örneği</span><span class="sxs-lookup"><span data-stu-id="578ca-308">Literal text example</span></span>  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-the-body-as-a-string-note-that-we-are-preserving-the-original-request-body-so-that-we-can-access-it-later-in-the-pipeline"></a><span data-ttu-id="578ca-309">Örnek, dize olarak gövdesi erişme.</span><span class="sxs-lookup"><span data-stu-id="578ca-309">Example accessing the body as a string.</span></span> <span data-ttu-id="578ca-310">Böylece biz ardışık düzeninde erişebilir biz özgün istek gövdesi koruma olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="578ca-310">Note that we are preserving the original request body so that we can access it later in the pipeline.</span></span>
  
```xml  
<set-body>  
@{   
    string inBody = context.Request.Body.As<string>(preserveContent: true);   
    if (inBody[0] =='c') {   
        inBody[0] = 'm';   
    }   
    return inBody;   
}  
</set-body>  
```  
  
#### <a name="example-accessing-the-body-as-a-jobject-note-that-since-we-are-not-reserving-the-original-request-body-accesing-it-later-in-the-pipeline-will-result-in-an-exception"></a><span data-ttu-id="578ca-311">Örnek, gövde bir JObject olarak erişme.</span><span class="sxs-lookup"><span data-stu-id="578ca-311">Example accessing the body as a JObject.</span></span> <span data-ttu-id="578ca-312">Biz özgün istek gövdesi, bunu daha sonra düzenindeki bir özel durumla sonuçlanır belirtilmemelidir ayırma değil bu yana unutmayın.</span><span class="sxs-lookup"><span data-stu-id="578ca-312">Note that since we are not reserving the original request body, accesing it later in the pipeline will result in an exception.</span></span>  
  
```xml  
<set-body>   
@{   
    JObject inBody = context.Request.Body.As<JObject>();   
    if (inBody.attribute == <tag>) {   
        inBody[0] = 'm';   
    }   
    return inBody.ToString();   
}   
</set-body>  
  
```  
  
#### <a name="filter-response-based-on-product"></a><span data-ttu-id="578ca-313">Ürüne göre filtre yanıtı</span><span class="sxs-lookup"><span data-stu-id="578ca-313">Filter response based on product</span></span>  
 <span data-ttu-id="578ca-314">Bu örnek veri öğeleri kullanırken arka uç hizmetinden alınan yanıtı kaldırarak içerik filtreleme gerçekleştirmek nasıl gösterir `Starter` ürün.</span><span class="sxs-lookup"><span data-stu-id="578ca-314">This example shows how to perform content filtering by removing data elements from the response received from the backend service when using the `Starter` product.</span></span> <span data-ttu-id="578ca-315">Yapılandırma ve bu ilkeyi kullanan bir örnek için bkz: [bulut kapak bölüm 177: daha Vlad Vinogradsky ile yönetim özelliklerini API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) ve 34:30 için ileri sarma.</span><span class="sxs-lookup"><span data-stu-id="578ca-315">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 34:30.</span></span> <span data-ttu-id="578ca-316">Genel bir bakış görmek 31:50 Başlat [tahmin koyu Sky API](https://developer.forecast.io/) bu tanıtım için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="578ca-316">Start  at 31:50 to see an overview of [The Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
```xml  
<!-- Copy this snippet into the outbound section to remove a number of data elements from the response received from the backend service based on the name of the api product -->  
<choose>  
  <when condition="@(context.Response.StatusCode == 200 && context.Product.Name.Equals("Starter"))">  
    <set-body>@{  
        var response = context.Response.Body.As<JObject>();  
        foreach (var key in new [] {"minutely", "hourly", "daily", "flags"}) {  
          response.Property (key).Remove ();  
        }  
        return response.ToString();  
      }  
    </set-body>  
  </when>  
</choose>  
```  

### <a name="using-liquid-templates-with-set-body"></a><span data-ttu-id="578ca-317">Set gövde ile sıvı şablonlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="578ca-317">Using Liquid templates with set body</span></span> 
<span data-ttu-id="578ca-318">`set-body` İlkesi kullanmak üzere yapılandırılabilir [sıvı](https://shopify.github.io/liquid/basics/introduction/) transfom bir istek veya yanıt gövdesi için şablon dili.</span><span class="sxs-lookup"><span data-stu-id="578ca-318">The `set-body` policy can be configured to use the [Liquid](https://shopify.github.io/liquid/basics/introduction/) templating language to transfom the body of a request or response.</span></span> <span data-ttu-id="578ca-319">Bu, ileti biçimi tamamen yeniden şekillendirmek gerekiyorsa çok etkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="578ca-319">This can be very effective if you need to completely reshape the format of your message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="578ca-320">Sıvı uyarlamasını kullanılan `set-body` ilke ', C# modu' yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="578ca-320">The implementation of Liquid used in the `set-body` policy is configured in 'C# mode'.</span></span> <span data-ttu-id="578ca-321">Bu filtreleme gibi şeyler yaparken özellikle önemlidir.</span><span class="sxs-lookup"><span data-stu-id="578ca-321">This is particularly important when doing things such as filtering.</span></span> <span data-ttu-id="578ca-322">Örnek olarak, bir tarih filtresi kullanarak Pascal kullanılmasını gerektiren büyük/küçük harf ve C# tarih biçimlendirme örn:</span><span class="sxs-lookup"><span data-stu-id="578ca-322">As an example, using a date filter requires the use of Pascal casing and C# date formatting e.g.:</span></span>
>
> <span data-ttu-id="578ca-323">{{body.foo.startDateTime| Tarih: "yyyyMMddTHH:mm:ddZ"}}</span><span class="sxs-lookup"><span data-stu-id="578ca-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span></span>

> [!IMPORTANT]
> <span data-ttu-id="578ca-324">Doğru sıvı şablonu kullanarak bir XML gövdesi bağlamak amacıyla kullanmak bir `set-header` Content-Type ayarlamak için ilke ya da uygulama/xml, text/xml (veya tüm ile biten türü + xml) için; JSON gövdesi, uygulama/json olmalıdır metin/json (veya ile biten herhangi bir türü + JSON).</span><span class="sxs-lookup"><span data-stu-id="578ca-324">In order to correctly bind to an XML body using the Liquid template, use a `set-header` policy to set Content-Type to either application/xml, text/xml (or any type ending with +xml); for a JSON body, it must be application/json, text/json (or any type ending with +json).</span></span>

#### <a name="convert-json-to-soap-using-a-liquid-template"></a><span data-ttu-id="578ca-325">JSON sıvı bir şablon kullanarak SOAP Dönüştür</span><span class="sxs-lookup"><span data-stu-id="578ca-325">Convert JSON to SOAP using a Liquid template</span></span>
```xml
<set-body template="liquid">
    <soap:Envelope xmlns="http://tempuri.org/" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:Body>
            <GetOpenOrders>
                <cust>{{body.getOpenOrders.cust}}</cust>
            </GetOpenOrders>
        </soap:Body>
    </soap:Envelope>
</set-body>
```

#### <a name="tranform-json-using-a-liquid-template"></a><span data-ttu-id="578ca-326">Dönüşüm sıvı bir şablon kullanarak JSON</span><span class="sxs-lookup"><span data-stu-id="578ca-326">Tranform JSON using a Liquid template</span></span>
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a><span data-ttu-id="578ca-327">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="578ca-327">Elements</span></span>  
  
|<span data-ttu-id="578ca-328">Ad</span><span class="sxs-lookup"><span data-stu-id="578ca-328">Name</span></span>|<span data-ttu-id="578ca-329">Açıklama</span><span class="sxs-lookup"><span data-stu-id="578ca-329">Description</span></span>|<span data-ttu-id="578ca-330">Gerekli</span><span class="sxs-lookup"><span data-stu-id="578ca-330">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="578ca-331">set-gövdesi</span><span class="sxs-lookup"><span data-stu-id="578ca-331">set-body</span></span>|<span data-ttu-id="578ca-332">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="578ca-332">Root element.</span></span> <span data-ttu-id="578ca-333">Gövde metin ya da body döndüren bir ifade içeriyor.</span><span class="sxs-lookup"><span data-stu-id="578ca-333">Contains the body text or an expressions that returns a body.</span></span>|<span data-ttu-id="578ca-334">Evet</span><span class="sxs-lookup"><span data-stu-id="578ca-334">Yes</span></span>|  

### <a name="properties"></a><span data-ttu-id="578ca-335">Özellikler</span><span class="sxs-lookup"><span data-stu-id="578ca-335">Properties</span></span>  
  
|<span data-ttu-id="578ca-336">Ad</span><span class="sxs-lookup"><span data-stu-id="578ca-336">Name</span></span>|<span data-ttu-id="578ca-337">Açıklama</span><span class="sxs-lookup"><span data-stu-id="578ca-337">Description</span></span>|<span data-ttu-id="578ca-338">Gerekli</span><span class="sxs-lookup"><span data-stu-id="578ca-338">Required</span></span>|<span data-ttu-id="578ca-339">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="578ca-339">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="578ca-340">şablon</span><span class="sxs-lookup"><span data-stu-id="578ca-340">template</span></span>|<span data-ttu-id="578ca-341">Gövde ilkesini ayarlama çalışacak şablon modunu değiştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="578ca-341">Used to change the templating mode that the set body policy will run in.</span></span> <span data-ttu-id="578ca-342">Şu anda desteklenen tek değerdir:</span><span class="sxs-lookup"><span data-stu-id="578ca-342">Currently the only supported value is:</span></span><br /><br /><span data-ttu-id="578ca-343">-Sıvı - gövde ilkesini ayarlama sıvı şablon altyapısı da kullanır</span><span class="sxs-lookup"><span data-stu-id="578ca-343">- liquid - the set body policy will use the liquid templating engine</span></span> |<span data-ttu-id="578ca-344">Hayır</span><span class="sxs-lookup"><span data-stu-id="578ca-344">No</span></span>|<span data-ttu-id="578ca-345">Sıvı</span><span class="sxs-lookup"><span data-stu-id="578ca-345">liquid</span></span>|  

<span data-ttu-id="578ca-346">İstek ve yanıt bilgilerine erişmek için sıvı şablon aşağıdaki özelliklere sahip bir bağlam nesnesi bağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="578ca-346">For accessing information about the request and response, the Liquid template can bind to a context object with the following properties:</span></span> <br />
<pre>context.
    Request.
        Url
        Method
        OriginalMethod
        OriginalUrl
        IpAddress
        MatchedParameters
        HasBody
        ClientCertificates
        Headers

    Response.
        StatusCode
        Method
        Headers
Url.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString

OriginalUrl.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString
</pre>



### <a name="usage"></a><span data-ttu-id="578ca-347">Kullanım</span><span class="sxs-lookup"><span data-stu-id="578ca-347">Usage</span></span>  
 <span data-ttu-id="578ca-348">Bu ilke aşağıdaki ilkesi kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="578ca-348">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="578ca-349">**İlke bölümleri:** gelen, giden arka uç</span><span class="sxs-lookup"><span data-stu-id="578ca-349">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="578ca-350">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="578ca-350">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="578ca-351"><a name="SetHTTPheader"></a>HTTP üstbilgisi kümesi</span><span class="sxs-lookup"><span data-stu-id="578ca-351"><a name="SetHTTPheader"></a> Set HTTP header</span></span>  
 <span data-ttu-id="578ca-352">`set-header` İlke değer atayan bir varolan yanıt ve/veya istek üstbilgisi veya yeni bir yanıt ve/veya istek üstbilgisi ekler.</span><span class="sxs-lookup"><span data-stu-id="578ca-352">The `set-header` policy assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
 <span data-ttu-id="578ca-353">HTTP üstbilgilerin listesi HTTP iletisine ekler.</span><span class="sxs-lookup"><span data-stu-id="578ca-353">Inserts a list of HTTP headers into an HTTP message.</span></span> <span data-ttu-id="578ca-354">Bir gelen ardışık düzeninde yerleştirildiğinde, bu ilkeyi hedef hizmete geçirilen İstek HTTP üstbilgilerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="578ca-354">When placed in an inbound pipeline, this policy sets the HTTP headers for the request being passed to the target service.</span></span> <span data-ttu-id="578ca-355">Giden ardışık düzeninde yerleştirildiğinde, bu ilke ağ geçidi'nin istemciye gönderilen yanıtı için HTTP üstbilgilerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="578ca-355">When placed in an outbound pipeline, this policy sets the HTTP headers for the response being sent to the gateway’s client.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="578ca-356">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="578ca-356">Policy statement</span></span>  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with the same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a><span data-ttu-id="578ca-357">Örnekler</span><span class="sxs-lookup"><span data-stu-id="578ca-357">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="578ca-358">Örnek</span><span class="sxs-lookup"><span data-stu-id="578ca-358">Example</span></span>  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-to-the-backend-service"></a><span data-ttu-id="578ca-359">Arka uç hizmetine bağlam bilgilerini ilet</span><span class="sxs-lookup"><span data-stu-id="578ca-359">Forward context information to the backend service</span></span>  
 <span data-ttu-id="578ca-360">Bu örnek, arka uç hizmetine bağlam bilgilerini sağlamak için API düzeyinde ilkeyi uygulamak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="578ca-360">This example shows how to apply policy at the API level to supply context information to the backend service.</span></span> <span data-ttu-id="578ca-361">Yapılandırma ve bu ilkeyi kullanan bir örnek için bkz: [bulut kapak bölüm 177: daha Vlad Vinogradsky ile yönetim özelliklerini API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) ve 10:30 için ileri sarma.</span><span class="sxs-lookup"><span data-stu-id="578ca-361">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 10:30.</span></span> <span data-ttu-id="578ca-362">12:10 işyerindeki İlkesi görebileceğiniz bir işlem Geliştirici Portalı'nda arama demo yoktur.</span><span class="sxs-lookup"><span data-stu-id="578ca-362">At 12:10 there is a demo of calling an operation in the developer portal where you can see the policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into the inbound element to forward some context information, user id and the region the gateway is hosted in, to the backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 <span data-ttu-id="578ca-363">Daha fazla bilgi için bkz: [ilke ifadelerini](api-management-policy-expressions.md) ve [bağlamının](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="578ca-363">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="578ca-364">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="578ca-364">Elements</span></span>  
  
|<span data-ttu-id="578ca-365">Ad</span><span class="sxs-lookup"><span data-stu-id="578ca-365">Name</span></span>|<span data-ttu-id="578ca-366">Açıklama</span><span class="sxs-lookup"><span data-stu-id="578ca-366">Description</span></span>|<span data-ttu-id="578ca-367">Gerekli</span><span class="sxs-lookup"><span data-stu-id="578ca-367">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="578ca-368">set üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="578ca-368">set-header</span></span>|<span data-ttu-id="578ca-369">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="578ca-369">Root element.</span></span>|<span data-ttu-id="578ca-370">Evet</span><span class="sxs-lookup"><span data-stu-id="578ca-370">Yes</span></span>|  
|<span data-ttu-id="578ca-371">değer</span><span class="sxs-lookup"><span data-stu-id="578ca-371">value</span></span>|<span data-ttu-id="578ca-372">Ayarlanacak üstbilgi değerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="578ca-372">Specifies the value of the header to be set.</span></span> <span data-ttu-id="578ca-373">Aynı ada sahip birden çok üstbilgi ek eklemek için `value` öğeleri.</span><span class="sxs-lookup"><span data-stu-id="578ca-373">For multiple headers with the same name add additional `value` elements.</span></span>|<span data-ttu-id="578ca-374">Evet</span><span class="sxs-lookup"><span data-stu-id="578ca-374">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="578ca-375">Özellikler</span><span class="sxs-lookup"><span data-stu-id="578ca-375">Properties</span></span>  
  
|<span data-ttu-id="578ca-376">Ad</span><span class="sxs-lookup"><span data-stu-id="578ca-376">Name</span></span>|<span data-ttu-id="578ca-377">Açıklama</span><span class="sxs-lookup"><span data-stu-id="578ca-377">Description</span></span>|<span data-ttu-id="578ca-378">Gerekli</span><span class="sxs-lookup"><span data-stu-id="578ca-378">Required</span></span>|<span data-ttu-id="578ca-379">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="578ca-379">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="578ca-380">Mevcut eylem</span><span class="sxs-lookup"><span data-stu-id="578ca-380">exists-action</span></span>|<span data-ttu-id="578ca-381">Üstbilgi zaten belirtildiğinde gerçekleştirilecek eylemi belirtir.</span><span class="sxs-lookup"><span data-stu-id="578ca-381">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="578ca-382">Bu öznitelik aşağıdaki değerlerden birine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="578ca-382">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="578ca-383">-Geçersiz Kıl - varolan üstbilgisinin değerini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="578ca-383">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="578ca-384">-skip - varolan üstbilgi değeri değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="578ca-384">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="578ca-385">-Ekle - Varolan üstbilgi değeri değer ekler.</span><span class="sxs-lookup"><span data-stu-id="578ca-385">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="578ca-386">-delete - istekten üstbilgiyi kaldırır.</span><span class="sxs-lookup"><span data-stu-id="578ca-386">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="578ca-387">Ayarlandığında `override` aynı ada sahip birden çok girdi kaydetme sonuçları (birden çok kez listelenir) tüm girdisi göre ayarlanan üstbilgisinde; yalnızca listelenen değerler sonuç ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="578ca-387">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="578ca-388">Hayır</span><span class="sxs-lookup"><span data-stu-id="578ca-388">No</span></span>|<span data-ttu-id="578ca-389">geçersiz kılma</span><span class="sxs-lookup"><span data-stu-id="578ca-389">override</span></span>|  
|<span data-ttu-id="578ca-390">ad</span><span class="sxs-lookup"><span data-stu-id="578ca-390">name</span></span>|<span data-ttu-id="578ca-391">Ayarlanacak üstbilginin adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="578ca-391">Specifies name of the header to be set.</span></span>|<span data-ttu-id="578ca-392">Evet</span><span class="sxs-lookup"><span data-stu-id="578ca-392">Yes</span></span>|<span data-ttu-id="578ca-393">Yok</span><span class="sxs-lookup"><span data-stu-id="578ca-393">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="578ca-394">Kullanım</span><span class="sxs-lookup"><span data-stu-id="578ca-394">Usage</span></span>  
 <span data-ttu-id="578ca-395">Bu ilke aşağıdaki ilkesi kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="578ca-395">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="578ca-396">**İlke bölümleri:** gelen, giden arka uç, hata</span><span class="sxs-lookup"><span data-stu-id="578ca-396">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="578ca-397">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="578ca-397">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="578ca-398"><a name="SetQueryStringParameter"></a>Set sorgu dizesi parametresi</span><span class="sxs-lookup"><span data-stu-id="578ca-398"><a name="SetQueryStringParameter"></a> Set query string parameter</span></span>  
 <span data-ttu-id="578ca-399">`set-query-parameter` İlkesi ekler, değiştirir değeri, veya silme isteği sorgu dizesi parametresi.</span><span class="sxs-lookup"><span data-stu-id="578ca-399">The `set-query-parameter` policy adds, replaces value of, or deletes request query string parameter.</span></span> <span data-ttu-id="578ca-400">Hiçbir zaman istekte mevcut veya sorgu parametreleri, isteğe bağlı olan arka uç hizmeti tarafından beklenen geçirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="578ca-400">Can be used to pass query parameters expected by the backend service which are optional or never present in the request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="578ca-401">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="578ca-401">Policy statement</span></span>  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with the same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a><span data-ttu-id="578ca-402">Örnekler</span><span class="sxs-lookup"><span data-stu-id="578ca-402">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="578ca-403">Örnek</span><span class="sxs-lookup"><span data-stu-id="578ca-403">Example</span></span>  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with the same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-to-the-backend-service"></a><span data-ttu-id="578ca-404">Arka uç hizmetine bağlam bilgilerini ilet</span><span class="sxs-lookup"><span data-stu-id="578ca-404">Forward context information to the backend service</span></span>  
 <span data-ttu-id="578ca-405">Bu örnek, arka uç hizmetine bağlam bilgilerini sağlamak için API düzeyinde ilkeyi uygulamak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="578ca-405">This example shows how to apply policy at the API level to supply context information to the backend service.</span></span> <span data-ttu-id="578ca-406">Yapılandırma ve bu ilkeyi kullanan bir örnek için bkz: [bulut kapak bölüm 177: daha Vlad Vinogradsky ile yönetim özelliklerini API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) ve 10:30 için ileri sarma.</span><span class="sxs-lookup"><span data-stu-id="578ca-406">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 10:30.</span></span> <span data-ttu-id="578ca-407">12:10 işyerindeki İlkesi görebileceğiniz bir işlem Geliştirici Portalı'nda arama demo yoktur.</span><span class="sxs-lookup"><span data-stu-id="578ca-407">At 12:10 there is a demo of calling an operation in the developer portal where you can see the policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into the inbound element to forward a piece of context, product name in this example, to the backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 <span data-ttu-id="578ca-408">Daha fazla bilgi için bkz: [ilke ifadelerini](api-management-policy-expressions.md) ve [bağlamının](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="578ca-408">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="578ca-409">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="578ca-409">Elements</span></span>  
  
|<span data-ttu-id="578ca-410">Ad</span><span class="sxs-lookup"><span data-stu-id="578ca-410">Name</span></span>|<span data-ttu-id="578ca-411">Açıklama</span><span class="sxs-lookup"><span data-stu-id="578ca-411">Description</span></span>|<span data-ttu-id="578ca-412">Gerekli</span><span class="sxs-lookup"><span data-stu-id="578ca-412">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="578ca-413">kümesi sorgu parametresi</span><span class="sxs-lookup"><span data-stu-id="578ca-413">set-query-parameter</span></span>|<span data-ttu-id="578ca-414">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="578ca-414">Root element.</span></span>|<span data-ttu-id="578ca-415">Evet</span><span class="sxs-lookup"><span data-stu-id="578ca-415">Yes</span></span>|  
|<span data-ttu-id="578ca-416">değer</span><span class="sxs-lookup"><span data-stu-id="578ca-416">value</span></span>|<span data-ttu-id="578ca-417">Ayarlanacak sorgu parametresinin değeri belirtir.</span><span class="sxs-lookup"><span data-stu-id="578ca-417">Specifies the value of the query parameter to be set.</span></span> <span data-ttu-id="578ca-418">Aynı ada sahip birden çok sorgu parametreleri ek eklemek için `value` öğeleri.</span><span class="sxs-lookup"><span data-stu-id="578ca-418">For multiple query parameters with the same name add additional `value` elements.</span></span>|<span data-ttu-id="578ca-419">Evet</span><span class="sxs-lookup"><span data-stu-id="578ca-419">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="578ca-420">Özellikler</span><span class="sxs-lookup"><span data-stu-id="578ca-420">Properties</span></span>  
  
|<span data-ttu-id="578ca-421">Ad</span><span class="sxs-lookup"><span data-stu-id="578ca-421">Name</span></span>|<span data-ttu-id="578ca-422">Açıklama</span><span class="sxs-lookup"><span data-stu-id="578ca-422">Description</span></span>|<span data-ttu-id="578ca-423">Gerekli</span><span class="sxs-lookup"><span data-stu-id="578ca-423">Required</span></span>|<span data-ttu-id="578ca-424">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="578ca-424">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="578ca-425">Mevcut eylem</span><span class="sxs-lookup"><span data-stu-id="578ca-425">exists-action</span></span>|<span data-ttu-id="578ca-426">Sorgu parametresi zaten belirtildiğinde gerçekleştirilecek eylemi belirtir.</span><span class="sxs-lookup"><span data-stu-id="578ca-426">Specifies what action to take when the query parameter is already specified.</span></span> <span data-ttu-id="578ca-427">Bu öznitelik aşağıdaki değerlerden birine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="578ca-427">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="578ca-428">-Geçersiz Kıl - varolan parametresinin değerini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="578ca-428">-   override - replaces the value of the existing parameter.</span></span><br /><span data-ttu-id="578ca-429">-skip - varolan sorgusu parametre değeri değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="578ca-429">-   skip - does not replace the existing query parameter value.</span></span><br /><span data-ttu-id="578ca-430">-Ekle - Varolan sorgu parametresi değeri değer ekler.</span><span class="sxs-lookup"><span data-stu-id="578ca-430">-   append - appends the value to the existing query parameter value.</span></span><br /><span data-ttu-id="578ca-431">-delete - sorgu parametresi istekten kaldırır.</span><span class="sxs-lookup"><span data-stu-id="578ca-431">-   delete - removes the query parameter from the request.</span></span><br /><br /> <span data-ttu-id="578ca-432">Ayarlandığında `override` aynı ada sahip birden çok girdi kaydetme sonuçlanıyor (birden çok kez listelenir) tüm girdisi göre ayarlanan sorgu parametresi; yalnızca listelenen değerler sonuç ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="578ca-432">When set to `override` enlisting multiple entries with the same name results in the query parameter being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="578ca-433">Hayır</span><span class="sxs-lookup"><span data-stu-id="578ca-433">No</span></span>|<span data-ttu-id="578ca-434">geçersiz kılma</span><span class="sxs-lookup"><span data-stu-id="578ca-434">override</span></span>|  
|<span data-ttu-id="578ca-435">ad</span><span class="sxs-lookup"><span data-stu-id="578ca-435">name</span></span>|<span data-ttu-id="578ca-436">Ayarlanacak sorgu parametresi adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="578ca-436">Specifies name of the query parameter to be set.</span></span>|<span data-ttu-id="578ca-437">Evet</span><span class="sxs-lookup"><span data-stu-id="578ca-437">Yes</span></span>|<span data-ttu-id="578ca-438">Yok</span><span class="sxs-lookup"><span data-stu-id="578ca-438">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="578ca-439">Kullanım</span><span class="sxs-lookup"><span data-stu-id="578ca-439">Usage</span></span>  
 <span data-ttu-id="578ca-440">Bu ilke aşağıdaki ilkesi kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="578ca-440">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="578ca-441">**İlke bölümleri:** gelen, arka uç</span><span class="sxs-lookup"><span data-stu-id="578ca-441">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="578ca-442">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="578ca-442">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="578ca-443"><a name="RewriteURL"></a>URL yeniden yazma</span><span class="sxs-lookup"><span data-stu-id="578ca-443"><a name="RewriteURL"></a> Rewrite URL</span></span>  
 <span data-ttu-id="578ca-444">`rewrite-uri` İlkesi dönüştürür istek URL'si ortak formundan web hizmeti tarafından beklenen form aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="578ca-444">The `rewrite-uri` policy converts a request URL from its public form to the form expected by the web service, as shown in the following example.</span></span>  
  
-   <span data-ttu-id="578ca-445">Ortak URL-`http://api.example.com/storenumber/ordernumber`</span><span class="sxs-lookup"><span data-stu-id="578ca-445">Public URL - `http://api.example.com/storenumber/ordernumber`</span></span>  
  
-   <span data-ttu-id="578ca-446">İstek URL-`http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span><span class="sxs-lookup"><span data-stu-id="578ca-446">Request URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span></span>  
  
 <span data-ttu-id="578ca-447">Bu ilke, İnsan ve/veya tarayıcı kolay URL web hizmeti tarafından beklenen URL biçimine dönüştürülmesi gereken olduğunda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="578ca-447">This policy can be used when a human and/or browser-friendly URL should be transformed into the URL format expected by the web service.</span></span> <span data-ttu-id="578ca-448">Bu ilke yalnızca temiz URL'leri, RESTful URL'leri, kullanıcı dostu URL'leri veya bir sorgu dizesi içermiyor ve bunun yerine yalnızca kaynak (yolunu içeren zamanıyla ilgili yapısal URL'leri SEO dostu URL'leri gibi alternatif bir URL biçimi gösterme ulaştığında uygulanacak gerekiyor Şema ve yetkili sonra).</span><span class="sxs-lookup"><span data-stu-id="578ca-448">This policy only needs to be applied when exposing an alternative URL format, such as clean URLs, RESTful URLs, user-friendly URLs or SEO-friendly URLs that are purely structural URLs that do not contain a query string and instead contain only the path of the resource (after the scheme and the authority).</span></span> <span data-ttu-id="578ca-449">Bu genellikle estetik, kullanılabilirlik veya arama motoru iyileştirmesi (SEO) amacıyla yapılır.</span><span class="sxs-lookup"><span data-stu-id="578ca-449">This is often done for aesthetic, usability, or search engine optimization (SEO) purposes.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="578ca-450">İlkeyi kullanarak sorgu dizesi parametreleri yalnızca ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="578ca-450">You can only add query string parameters using the policy.</span></span> <span data-ttu-id="578ca-451">Ek şablon yol parametreleri yeniden yazma URL'de ekleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="578ca-451">You cannot add extra template path parameters in the rewrite URL.</span></span>  

### <a name="policy-statement"></a><span data-ttu-id="578ca-452">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="578ca-452">Policy statement</span></span>  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a><span data-ttu-id="578ca-453">Örnek</span><span class="sxs-lookup"><span data-stu-id="578ca-453">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/v2/US/hardware/{storenumber}&{ordernumber}?City=city&State=state" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set to /get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put?c=d -->
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set to /get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" copy-unmatched-params="false" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put -->
```

### <a name="elements"></a><span data-ttu-id="578ca-454">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="578ca-454">Elements</span></span>  
  
|<span data-ttu-id="578ca-455">Ad</span><span class="sxs-lookup"><span data-stu-id="578ca-455">Name</span></span>|<span data-ttu-id="578ca-456">Açıklama</span><span class="sxs-lookup"><span data-stu-id="578ca-456">Description</span></span>|<span data-ttu-id="578ca-457">Gerekli</span><span class="sxs-lookup"><span data-stu-id="578ca-457">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="578ca-458">yeniden yazma URI'sı</span><span class="sxs-lookup"><span data-stu-id="578ca-458">rewrite-uri</span></span>|<span data-ttu-id="578ca-459">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="578ca-459">Root element.</span></span>|<span data-ttu-id="578ca-460">Evet</span><span class="sxs-lookup"><span data-stu-id="578ca-460">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="578ca-461">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="578ca-461">Attributes</span></span>  
  
|<span data-ttu-id="578ca-462">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="578ca-462">Attribute</span></span>|<span data-ttu-id="578ca-463">Açıklama</span><span class="sxs-lookup"><span data-stu-id="578ca-463">Description</span></span>|<span data-ttu-id="578ca-464">Gerekli</span><span class="sxs-lookup"><span data-stu-id="578ca-464">Required</span></span>|<span data-ttu-id="578ca-465">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="578ca-465">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="578ca-466">şablon</span><span class="sxs-lookup"><span data-stu-id="578ca-466">template</span></span>|<span data-ttu-id="578ca-467">Herhangi bir sorgu dizesi parametre ile gerçek web hizmeti URL'si.</span><span class="sxs-lookup"><span data-stu-id="578ca-467">The actual web service URL with any query string parameters.</span></span> <span data-ttu-id="578ca-468">İfadeler kullanırken, tam değeri bir ifade olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="578ca-468">When using expressions, the whole value must be an expression.</span></span>|<span data-ttu-id="578ca-469">Evet</span><span class="sxs-lookup"><span data-stu-id="578ca-469">Yes</span></span>|<span data-ttu-id="578ca-470">Yok</span><span class="sxs-lookup"><span data-stu-id="578ca-470">N/A</span></span>|  
|<span data-ttu-id="578ca-471">kopya eşleşmeyen-parametreleri</span><span class="sxs-lookup"><span data-stu-id="578ca-471">copy-unmatched-params</span></span>|<span data-ttu-id="578ca-472">Özgün URL şablonunda mevcut değil gelen istekte sorgu parametreleri yeniden yazma şablon tarafından tanımlanan URL'ye eklenmiş olup olmadığını belirtir</span><span class="sxs-lookup"><span data-stu-id="578ca-472">Specifies whether query parameters in the incoming request not present in the original URL template are added to the URL defined by the re-write template</span></span>|<span data-ttu-id="578ca-473">Hayır</span><span class="sxs-lookup"><span data-stu-id="578ca-473">No</span></span>|<span data-ttu-id="578ca-474">TRUE</span><span class="sxs-lookup"><span data-stu-id="578ca-474">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="578ca-475">Kullanım</span><span class="sxs-lookup"><span data-stu-id="578ca-475">Usage</span></span>  
 <span data-ttu-id="578ca-476">Bu ilke aşağıdaki ilkesi kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="578ca-476">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="578ca-477">**İlke bölümleri:** gelen</span><span class="sxs-lookup"><span data-stu-id="578ca-477">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="578ca-478">**İlke kapsamları:** ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="578ca-478">**Policy scopes:** product, API, operation</span></span>  
  
##  <span data-ttu-id="578ca-479"><a name="XSLTransform"></a>XSLT kullanarak XML dönüştürme</span><span class="sxs-lookup"><span data-stu-id="578ca-479"><a name="XSLTransform"></a> Transform XML using an XSLT</span></span>  
 <span data-ttu-id="578ca-480">`Transform XML using an XSLT` İlke istek veya yanıt gövdesinde XML XSL dönüşümünü uygular.</span><span class="sxs-lookup"><span data-stu-id="578ca-480">The `Transform XML using an XSLT` policy applies an XSL transformation to XML in the request or response body.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="578ca-481">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="578ca-481">Policy statement</span></span>  
  
```xml  
<xsl-transform>  
    <parameter name="User-Agent">@(context.Request.Headers.GetValueOrDefault("User-Agent","non-specified"))</parameter>  
    <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
        <xsl:output method="xml" indent="yes" />  
        <xsl:param name="User-Agent" />  
        <xsl:template match="* | @* | node()">  
            <xsl:copy>  
                <xsl:if test="self::* and not(parent::*)">  
                    <xsl:attribute name="User-Agent">  
                        <xsl:value-of select="$User-Agent" />  
                    </xsl:attribute>  
                </xsl:if>  
                <xsl:apply-templates select="* | @* | node()" />  
            </xsl:copy>  
        </xsl:template>  
    </xsl:stylesheet>  
  </xsl-transform>  
```  
  
### <a name="example"></a><span data-ttu-id="578ca-482">Örnek</span><span class="sxs-lookup"><span data-stu-id="578ca-482">Example</span></span>  
  
```xml  
<policies>  
  <inbound>  
      <base />  
  </inbound>  
  <outbound>  
      <base />  
      <xsl-transform>  
        <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
            <xsl:output omit-xml-declaration="yes" method="xml" indent="yes" />  
            <!-- Copy all nodes directly-->  
            <xsl:template match="node()| @*|*">  
                <xsl:copy>  
                    <xsl:apply-templates select="@* | node()|*" />  
                </xsl:copy>  
            </xsl:template>  
        </xsl:stylesheet>  
    </xsl-transform>  
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="578ca-483">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="578ca-483">Elements</span></span>  
  
|<span data-ttu-id="578ca-484">Ad</span><span class="sxs-lookup"><span data-stu-id="578ca-484">Name</span></span>|<span data-ttu-id="578ca-485">Açıklama</span><span class="sxs-lookup"><span data-stu-id="578ca-485">Description</span></span>|<span data-ttu-id="578ca-486">Gerekli</span><span class="sxs-lookup"><span data-stu-id="578ca-486">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="578ca-487">XSL Dönüştürme</span><span class="sxs-lookup"><span data-stu-id="578ca-487">xsl-transform</span></span>|<span data-ttu-id="578ca-488">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="578ca-488">Root element.</span></span>|<span data-ttu-id="578ca-489">Evet</span><span class="sxs-lookup"><span data-stu-id="578ca-489">Yes</span></span>|  
|<span data-ttu-id="578ca-490">Parametre</span><span class="sxs-lookup"><span data-stu-id="578ca-490">parameter</span></span>|<span data-ttu-id="578ca-491">Dönüşüm dosyasında kullanılan değişkenler tanımlamak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="578ca-491">Used to define variables used in the transform</span></span>|<span data-ttu-id="578ca-492">Hayır</span><span class="sxs-lookup"><span data-stu-id="578ca-492">No</span></span>|  
|<span data-ttu-id="578ca-493">stylesheet</span><span class="sxs-lookup"><span data-stu-id="578ca-493">xsl:stylesheet</span></span>|<span data-ttu-id="578ca-494">Kök stil öğesi.</span><span class="sxs-lookup"><span data-stu-id="578ca-494">Root stylesheet element.</span></span> <span data-ttu-id="578ca-495">Tüm öğeleri ve özniteliklerinin içinde tanımlanan standarda [XSLT belirtimi](http://www.w3.org/TR/xslt)</span><span class="sxs-lookup"><span data-stu-id="578ca-495">All elements and attributes defined within follow the standard [XSLT specification](http://www.w3.org/TR/xslt)</span></span>|<span data-ttu-id="578ca-496">Evet</span><span class="sxs-lookup"><span data-stu-id="578ca-496">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="578ca-497">Kullanım</span><span class="sxs-lookup"><span data-stu-id="578ca-497">Usage</span></span>  
 <span data-ttu-id="578ca-498">Bu ilke aşağıdaki ilkesi kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="578ca-498">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="578ca-499">**İlke bölümleri:** gelen, giden</span><span class="sxs-lookup"><span data-stu-id="578ca-499">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="578ca-500">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="578ca-500">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="578ca-501">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="578ca-501">Next steps</span></span>
<span data-ttu-id="578ca-502">İlkeleriyle çalışma daha fazla bilgi için bkz: [API Management ilkeleri](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="578ca-502">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
