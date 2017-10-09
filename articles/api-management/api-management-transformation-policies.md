---
title: "aaaAzure API Management dönüştürme ilkelerini | Microsoft Docs"
description: "Merhaba dönüştürme ilkelerini kullanılmak üzere Azure API Management hakkında bilgi edinin."
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
ms.openlocfilehash: 2891cc52d0017b717b3c12a98bc4941b5fd7ea78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-transformation-policies"></a><span data-ttu-id="d46f5-103">API Management dönüştürme ilkelerini</span><span class="sxs-lookup"><span data-stu-id="d46f5-103">API Management transformation policies</span></span>
<span data-ttu-id="d46f5-104">Bu konuda API Management ilkelere hello için bir başvuru sağlar.</span><span class="sxs-lookup"><span data-stu-id="d46f5-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="d46f5-105">Ekleme ve ilkeleri yapılandırma hakkında daha fazla bilgi için bkz: [API Management ilkeleri](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="d46f5-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="d46f5-106"><a name="TransformationPolicies"></a>Dönüştürme ilkelerini</span><span class="sxs-lookup"><span data-stu-id="d46f5-106"><a name="TransformationPolicies"></a> Transformation policies</span></span>  
  
-   <span data-ttu-id="d46f5-107">[JSON tooXML Dönüştür](api-management-transformation-policies.md#ConvertJSONtoXML) - dönüştürür istek veya yanıt gövdesi JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="d46f5-107">[Convert JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON tooXML.</span></span>  
  
-   <span data-ttu-id="d46f5-108">[XML tooJSON Dönüştür](api-management-transformation-policies.md#ConvertXMLtoJSON) - dönüştürür istek veya yanıt gövdesi XML tooJSON.</span><span class="sxs-lookup"><span data-stu-id="d46f5-108">[Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML tooJSON.</span></span>  
  
-   <span data-ttu-id="d46f5-109">[Bulma ve değiştirme dizesi gövdesi içinde](api-management-transformation-policies.md#Findandreplacestringinbody) - bir istek veya yanıt alt dizeyi bulur ve farklı bir dizeyle değiştirir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-109">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
-   <span data-ttu-id="d46f5-110">[İçeriği URL'leri maske](api-management-transformation-policies.md#MaskURLSContent) -(maskeleri)'yeniden yazar bağlantılar hello yanıt gövdesi böylece hello ağ geçidi aracılığıyla toohello eşdeğer bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="d46f5-110">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>  
  
-   <span data-ttu-id="d46f5-111">[Arka uç hizmetini ayarlamak](api-management-transformation-policies.md#SetBackendService) -değişiklikleri hello arka uç hizmetine gelen bir istek için.</span><span class="sxs-lookup"><span data-stu-id="d46f5-111">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes hello backend service for an incoming request.</span></span>  
  
-   <span data-ttu-id="d46f5-112">[Gövde ayarlamak](api-management-transformation-policies.md#SetBody) -hello ileti gövdesi gelen ve giden istekleri için ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d46f5-112">[Set body](api-management-transformation-policies.md#SetBody) - Sets hello message body for incoming and outgoing requests.</span></span>  
  
-   <span data-ttu-id="d46f5-113">[HTTP üstbilgisi kümesi](api-management-transformation-policies.md#SetHTTPheader) - değer tooan varolan yanıt ve/veya istek üstbilgisi atar veya yeni bir yanıt ve/veya istek üstbilgisi ekler.</span><span class="sxs-lookup"><span data-stu-id="d46f5-113">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
-   <span data-ttu-id="d46f5-114">[Sorgu dizesi parametresi kümesi](api-management-transformation-policies.md#SetQueryStringParameter) - ekler, değiştirir değerini veya istek sorgu dizesi parametresi siler.</span><span class="sxs-lookup"><span data-stu-id="d46f5-114">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
-   <span data-ttu-id="d46f5-115">[URL yeniden yazma](api-management-transformation-policies.md#RewriteURL) -hello web hizmeti tarafından beklenen genel form toohello formundan bir istek URL'sini dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="d46f5-115">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form toohello form expected by hello web service.</span></span>  
  
-   <span data-ttu-id="d46f5-116">[XSLT kullanarak XML dönüştürme](api-management-transformation-policies.md#XSLTransform) -bir XSL Dönüştürme tooXML hello istek veya yanıt gövdesi içinde geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-116">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
##  <span data-ttu-id="d46f5-117"><a name="ConvertJSONtoXML"></a>JSON tooXML Dönüştür</span><span class="sxs-lookup"><span data-stu-id="d46f5-117"><a name="ConvertJSONtoXML"></a> Convert JSON tooXML</span></span>  
 <span data-ttu-id="d46f5-118">Merhaba `json-to-xml` ilkeyi JSON tooXML bir istek veya yanıt gövdesi dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="d46f5-118">hello `json-to-xml` policy converts a request or response body from JSON tooXML.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d46f5-119">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="d46f5-119">Policy statement</span></span>  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="d46f5-120">Örnek</span><span class="sxs-lookup"><span data-stu-id="d46f5-120">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="d46f5-121">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="d46f5-121">Elements</span></span>  
  
|<span data-ttu-id="d46f5-122">Ad</span><span class="sxs-lookup"><span data-stu-id="d46f5-122">Name</span></span>|<span data-ttu-id="d46f5-123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d46f5-123">Description</span></span>|<span data-ttu-id="d46f5-124">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d46f5-124">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d46f5-125">JSON xml</span><span class="sxs-lookup"><span data-stu-id="d46f5-125">json-to-xml</span></span>|<span data-ttu-id="d46f5-126">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="d46f5-126">Root element.</span></span>|<span data-ttu-id="d46f5-127">Evet</span><span class="sxs-lookup"><span data-stu-id="d46f5-127">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d46f5-128">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="d46f5-128">Attributes</span></span>  
  
|<span data-ttu-id="d46f5-129">Ad</span><span class="sxs-lookup"><span data-stu-id="d46f5-129">Name</span></span>|<span data-ttu-id="d46f5-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d46f5-130">Description</span></span>|<span data-ttu-id="d46f5-131">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d46f5-131">Required</span></span>|<span data-ttu-id="d46f5-132">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="d46f5-132">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d46f5-133">Uygula</span><span class="sxs-lookup"><span data-stu-id="d46f5-133">apply</span></span>|<span data-ttu-id="d46f5-134">Merhaba öznitelik değerleri aşağıdaki hello tooone ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-134">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="d46f5-135">-her zaman - her zaman dönüştürme uygulanır.</span><span class="sxs-lookup"><span data-stu-id="d46f5-135">-   always - always apply conversion.</span></span><br /><span data-ttu-id="d46f5-136">Yalnızca yanıt Content-Type üstbilgisi JSON varlığını gösteriyorsa - içerik türü json - dönüştürülemiyor.</span><span class="sxs-lookup"><span data-stu-id="d46f5-136">-   content-type-json - convert only if response Content-Type header indicates presence of JSON.</span></span>|<span data-ttu-id="d46f5-137">Evet</span><span class="sxs-lookup"><span data-stu-id="d46f5-137">Yes</span></span>|<span data-ttu-id="d46f5-138">Yok</span><span class="sxs-lookup"><span data-stu-id="d46f5-138">N/A</span></span>|  
|<span data-ttu-id="d46f5-139">göz önünde bulundurun kabul-üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="d46f5-139">consider-accept-header</span></span>|<span data-ttu-id="d46f5-140">Merhaba öznitelik değerleri aşağıdaki hello tooone ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-140">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="d46f5-141">JSON istek Accept üstbilgisi isteniyorsa - true - dönüştürme uygulanır.</span><span class="sxs-lookup"><span data-stu-id="d46f5-141">-   true - apply conversion if JSON is requested in request Accept header.</span></span><br /><span data-ttu-id="d46f5-142">-false - her zaman dönüştürme uygulayın.</span><span class="sxs-lookup"><span data-stu-id="d46f5-142">-   false -always apply conversion.</span></span>|<span data-ttu-id="d46f5-143">Hayır</span><span class="sxs-lookup"><span data-stu-id="d46f5-143">No</span></span>|<span data-ttu-id="d46f5-144">TRUE</span><span class="sxs-lookup"><span data-stu-id="d46f5-144">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d46f5-145">Kullanım</span><span class="sxs-lookup"><span data-stu-id="d46f5-145">Usage</span></span>  
 <span data-ttu-id="d46f5-146">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d46f5-146">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d46f5-147">**İlke bölümleri:** gelen, giden, hata</span><span class="sxs-lookup"><span data-stu-id="d46f5-147">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="d46f5-148">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="d46f5-148">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d46f5-149"><a name="ConvertXMLtoJSON"></a>XML tooJSON Dönüştür</span><span class="sxs-lookup"><span data-stu-id="d46f5-149"><a name="ConvertXMLtoJSON"></a> Convert XML tooJSON</span></span>  
 <span data-ttu-id="d46f5-150">Merhaba `xml-to-json` ilkeyi XML tooJSON bir istek veya yanıt gövdesi dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="d46f5-150">hello `xml-to-json` policy converts a request or response body from XML tooJSON.</span></span> <span data-ttu-id="d46f5-151">Bu ilke API'leri yalnızca XML arka uç web hizmetlerini temel alarak kullanılan toomodernize olabilir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-151">This policy can be used toomodernize APIs based on XML-only backend web services.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d46f5-152">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="d46f5-152">Policy statement</span></span>  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="d46f5-153">Örnek</span><span class="sxs-lookup"><span data-stu-id="d46f5-153">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="d46f5-154">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="d46f5-154">Elements</span></span>  
  
|<span data-ttu-id="d46f5-155">Ad</span><span class="sxs-lookup"><span data-stu-id="d46f5-155">Name</span></span>|<span data-ttu-id="d46f5-156">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d46f5-156">Description</span></span>|<span data-ttu-id="d46f5-157">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d46f5-157">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d46f5-158">XML json</span><span class="sxs-lookup"><span data-stu-id="d46f5-158">xml-to-json</span></span>|<span data-ttu-id="d46f5-159">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="d46f5-159">Root element.</span></span>|<span data-ttu-id="d46f5-160">Evet</span><span class="sxs-lookup"><span data-stu-id="d46f5-160">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d46f5-161">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="d46f5-161">Attributes</span></span>  
  
|<span data-ttu-id="d46f5-162">Ad</span><span class="sxs-lookup"><span data-stu-id="d46f5-162">Name</span></span>|<span data-ttu-id="d46f5-163">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d46f5-163">Description</span></span>|<span data-ttu-id="d46f5-164">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d46f5-164">Required</span></span>|<span data-ttu-id="d46f5-165">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="d46f5-165">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d46f5-166">türü</span><span class="sxs-lookup"><span data-stu-id="d46f5-166">kind</span></span>|<span data-ttu-id="d46f5-167">Merhaba öznitelik değerleri aşağıdaki hello tooone ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-167">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="d46f5-168">-javascript kolay - hello dönüştürülen JSON bir form kolay tooJavaScript geliştiriciler sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-168">-   javascript-friendly - hello converted JSON has a form friendly tooJavaScript developers.</span></span><br /><span data-ttu-id="d46f5-169">-doğrudan - hello dönüştürülen JSON hello özgün XML belge yapısını yansıtır.</span><span class="sxs-lookup"><span data-stu-id="d46f5-169">-   direct - hello converted JSON reflects hello original XML document's structure.</span></span>|<span data-ttu-id="d46f5-170">Evet</span><span class="sxs-lookup"><span data-stu-id="d46f5-170">Yes</span></span>|<span data-ttu-id="d46f5-171">Yok</span><span class="sxs-lookup"><span data-stu-id="d46f5-171">N/A</span></span>|  
|<span data-ttu-id="d46f5-172">Uygula</span><span class="sxs-lookup"><span data-stu-id="d46f5-172">apply</span></span>|<span data-ttu-id="d46f5-173">Merhaba öznitelik değerleri aşağıdaki hello tooone ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-173">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="d46f5-174">-her zaman - her zaman dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="d46f5-174">-   always - convert always.</span></span><br /><span data-ttu-id="d46f5-175">Yalnızca yanıt Content-Type üstbilgisi XML varlığını gösteriyorsa - içerik türü xml - dönüştürülemiyor.</span><span class="sxs-lookup"><span data-stu-id="d46f5-175">-   content-type-xml - convert only if response Content-Type header indicates presence of XML.</span></span>|<span data-ttu-id="d46f5-176">Evet</span><span class="sxs-lookup"><span data-stu-id="d46f5-176">Yes</span></span>|<span data-ttu-id="d46f5-177">Yok</span><span class="sxs-lookup"><span data-stu-id="d46f5-177">N/A</span></span>|  
|<span data-ttu-id="d46f5-178">göz önünde bulundurun kabul-üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="d46f5-178">consider-accept-header</span></span>|<span data-ttu-id="d46f5-179">Merhaba öznitelik değerleri aşağıdaki hello tooone ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-179">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="d46f5-180">XML isteği Accept üstbilgisi isteniyorsa - true - dönüştürme uygulanır.</span><span class="sxs-lookup"><span data-stu-id="d46f5-180">-   true - apply conversion if XML is requested in request Accept header.</span></span><br /><span data-ttu-id="d46f5-181">-false - her zaman dönüştürme uygulayın.</span><span class="sxs-lookup"><span data-stu-id="d46f5-181">-   false -always apply conversion.</span></span>|<span data-ttu-id="d46f5-182">Hayır</span><span class="sxs-lookup"><span data-stu-id="d46f5-182">No</span></span>|<span data-ttu-id="d46f5-183">TRUE</span><span class="sxs-lookup"><span data-stu-id="d46f5-183">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d46f5-184">Kullanım</span><span class="sxs-lookup"><span data-stu-id="d46f5-184">Usage</span></span>  
 <span data-ttu-id="d46f5-185">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d46f5-185">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d46f5-186">**İlke bölümleri:** gelen, giden, hata</span><span class="sxs-lookup"><span data-stu-id="d46f5-186">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="d46f5-187">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="d46f5-187">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d46f5-188"><a name="Findandreplacestringinbody"></a>Bulma ve gövde dizesinde değiştirme</span><span class="sxs-lookup"><span data-stu-id="d46f5-188"><a name="Findandreplacestringinbody"></a> Find and replace string in body</span></span>  
 <span data-ttu-id="d46f5-189">Merhaba `find-and-replace` ilke isteği veya yanıtı alt dizeyi bulur ve farklı bir dizeyle değiştirir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-189">hello `find-and-replace` policy finds a request or response substring and replaces it with a different substring.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d46f5-190">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="d46f5-190">Policy statement</span></span>  
  
```xml  
<find-and-replace from="what tooreplace" to="replacement" />  
```  
  
### <a name="example"></a><span data-ttu-id="d46f5-191">Örnek</span><span class="sxs-lookup"><span data-stu-id="d46f5-191">Example</span></span>  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a><span data-ttu-id="d46f5-192">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="d46f5-192">Elements</span></span>  
  
|<span data-ttu-id="d46f5-193">Ad</span><span class="sxs-lookup"><span data-stu-id="d46f5-193">Name</span></span>|<span data-ttu-id="d46f5-194">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d46f5-194">Description</span></span>|<span data-ttu-id="d46f5-195">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d46f5-195">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d46f5-196">Bul ve Değiştir</span><span class="sxs-lookup"><span data-stu-id="d46f5-196">find-and-replace</span></span>|<span data-ttu-id="d46f5-197">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="d46f5-197">Root element.</span></span>|<span data-ttu-id="d46f5-198">Evet</span><span class="sxs-lookup"><span data-stu-id="d46f5-198">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d46f5-199">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="d46f5-199">Attributes</span></span>  
  
|<span data-ttu-id="d46f5-200">Ad</span><span class="sxs-lookup"><span data-stu-id="d46f5-200">Name</span></span>|<span data-ttu-id="d46f5-201">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d46f5-201">Description</span></span>|<span data-ttu-id="d46f5-202">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d46f5-202">Required</span></span>|<span data-ttu-id="d46f5-203">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="d46f5-203">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d46f5-204">Kaynak</span><span class="sxs-lookup"><span data-stu-id="d46f5-204">from</span></span>|<span data-ttu-id="d46f5-205">Merhaba dize toosearch için.</span><span class="sxs-lookup"><span data-stu-id="d46f5-205">hello string toosearch for.</span></span>|<span data-ttu-id="d46f5-206">Evet</span><span class="sxs-lookup"><span data-stu-id="d46f5-206">Yes</span></span>|<span data-ttu-id="d46f5-207">Yok</span><span class="sxs-lookup"><span data-stu-id="d46f5-207">N/A</span></span>|  
|<span data-ttu-id="d46f5-208">-</span><span class="sxs-lookup"><span data-stu-id="d46f5-208">to</span></span>|<span data-ttu-id="d46f5-209">Merhaba değiştirme dizesi.</span><span class="sxs-lookup"><span data-stu-id="d46f5-209">hello replacement string.</span></span> <span data-ttu-id="d46f5-210">Sıfır uzunluk değiştirme dizesi tooremove hello arama dizesi belirtin.</span><span class="sxs-lookup"><span data-stu-id="d46f5-210">Specify a zero length replacement string tooremove hello search string.</span></span>|<span data-ttu-id="d46f5-211">Evet</span><span class="sxs-lookup"><span data-stu-id="d46f5-211">Yes</span></span>|<span data-ttu-id="d46f5-212">Yok</span><span class="sxs-lookup"><span data-stu-id="d46f5-212">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d46f5-213">Kullanım</span><span class="sxs-lookup"><span data-stu-id="d46f5-213">Usage</span></span>  
 <span data-ttu-id="d46f5-214">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d46f5-214">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d46f5-215">**İlke bölümleri:** gelen, giden arka uç, hata</span><span class="sxs-lookup"><span data-stu-id="d46f5-215">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="d46f5-216">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="d46f5-216">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d46f5-217"><a name="MaskURLSContent"></a>İçerik maskesi URL'leri</span><span class="sxs-lookup"><span data-stu-id="d46f5-217"><a name="MaskURLSContent"></a> Mask URLs in content</span></span>  
 <span data-ttu-id="d46f5-218">Merhaba `redirect-content-urls` İlkesi hello ağ geçidi aracılığıyla toohello eşdeğer bağlantı noktası böylece hello yanıt gövdesi (maskeleri) bağlantıları yeniden yazar.</span><span class="sxs-lookup"><span data-stu-id="d46f5-218">hello `redirect-content-urls` policy re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span> <span data-ttu-id="d46f5-219">Merhaba giden bölüm toore yazma yanıt gövdesi bağlantılar toomake bunları noktası toohello ağ geçidi kullanın.</span><span class="sxs-lookup"><span data-stu-id="d46f5-219">Use in hello outbound section toore-write response body links toomake them point toohello gateway.</span></span> <span data-ttu-id="d46f5-220">Merhaba kullanımda gelen ters efekt bölümü.</span><span class="sxs-lookup"><span data-stu-id="d46f5-220">Use in hello inbound section for an opposite effect.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="d46f5-221">Bu ilke tüm üstbilgi değerleri gibi değiştirmez `Location` üstbilgileri.</span><span class="sxs-lookup"><span data-stu-id="d46f5-221">This policy does not change any header values such as `Location` headers.</span></span> <span data-ttu-id="d46f5-222">toochange üstbilgi değerleri kullanmak hello [set üstbilgisi](api-management-transformation-policies.md#SetHTTPheader) ilkesi.</span><span class="sxs-lookup"><span data-stu-id="d46f5-222">toochange header values, use hello [set-header](api-management-transformation-policies.md#SetHTTPheader) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d46f5-223">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="d46f5-223">Policy statement</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a><span data-ttu-id="d46f5-224">Örnek</span><span class="sxs-lookup"><span data-stu-id="d46f5-224">Example</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a><span data-ttu-id="d46f5-225">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="d46f5-225">Elements</span></span>  
  
|<span data-ttu-id="d46f5-226">Ad</span><span class="sxs-lookup"><span data-stu-id="d46f5-226">Name</span></span>|<span data-ttu-id="d46f5-227">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d46f5-227">Description</span></span>|<span data-ttu-id="d46f5-228">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d46f5-228">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d46f5-229">Yönlendirme içerik URL'leri</span><span class="sxs-lookup"><span data-stu-id="d46f5-229">redirect-content-urls</span></span>|<span data-ttu-id="d46f5-230">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="d46f5-230">Root element.</span></span>|<span data-ttu-id="d46f5-231">Evet</span><span class="sxs-lookup"><span data-stu-id="d46f5-231">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d46f5-232">Kullanım</span><span class="sxs-lookup"><span data-stu-id="d46f5-232">Usage</span></span>  
 <span data-ttu-id="d46f5-233">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d46f5-233">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d46f5-234">**İlke bölümleri:** gelen, giden</span><span class="sxs-lookup"><span data-stu-id="d46f5-234">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="d46f5-235">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="d46f5-235">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d46f5-236"><a name="SetBackendService"></a>Arka uç hizmet belirleme</span><span class="sxs-lookup"><span data-stu-id="d46f5-236"><a name="SetBackendService"></a> Set backend service</span></span>  
 <span data-ttu-id="d46f5-237">Kullanım hello `set-backend-service` İlkesi tooredirect gelen bir istek tooa farklı arka uç bir hello API ayarları bu işlem için belirtilen hello daha.</span><span class="sxs-lookup"><span data-stu-id="d46f5-237">Use hello `set-backend-service` policy tooredirect an incoming request tooa different backend than hello one specified in hello API settings for that operation.</span></span> <span data-ttu-id="d46f5-238">Bu ilke hello arka uç hizmeti temel URL'sini hello gelen isteği toohello bir hello İlkesi'nde belirtilen değiştirir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-238">This policy changes hello backend service base URL of hello incoming request toohello one specified in hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d46f5-239">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="d46f5-239">Policy statement</span></span>  
  
```xml  
<set-backend-service base-url="base URL of hello backend service" />  
```  
  
### <a name="example"></a><span data-ttu-id="d46f5-240">Örnek</span><span class="sxs-lookup"><span data-stu-id="d46f5-240">Example</span></span>  
  
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
<span data-ttu-id="d46f5-241">Bu örnek hello arka uç hizmeti ilkesini ayarlama hello sorgu dizesi tooa farklı arka uç hizmeti hello bir belirtilen hello API'den geçirilen hello sürüm değere göre isteklerini yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-241">In this example hello set backend service policy routes requests based on hello version value passed in hello query string tooa different backend service than hello one specified in hello API.</span></span>
  
<span data-ttu-id="d46f5-242">Başlangıçta hello arka uç hizmeti temel URL'si hello API ayarlarından türetilir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-242">Initially hello backend service base URL is derived from hello API settings.</span></span> <span data-ttu-id="d46f5-243">Böylece istek URL'si hello `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` hale `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` burada `http://contoso.com/api/10.4/` hello API ayarlarında belirtilen hello arka uç hizmeti URL.</span><span class="sxs-lookup"><span data-stu-id="d46f5-243">So hello request URL `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` becomes `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` where `http://contoso.com/api/10.4/` is hello backend service URL specified in hello API settings.</span></span>  
  
<span data-ttu-id="d46f5-244">Ne zaman hello [< seçin\> ](api-management-advanced-policies.md#choose) ilke bildirimi uygulanır hello arka uç hizmeti temel URL'si değişebilir yeniden ya da çok`http://contoso.com/api/8.2` veya `http://contoso.com/api/9.1`hello hello sürüm istek sorgu parametresinin değerini bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="d46f5-244">When hello [<choose\>](api-management-advanced-policies.md#choose) policy statement is applied hello backend service base URL may change again either too`http://contoso.com/api/8.2` or `http://contoso.com/api/9.1`, depending on hello value of hello version request query parameter.</span></span> <span data-ttu-id="d46f5-245">Örneğin, hello değer ise `"2013-15"` hello son istek URL'si hale `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span><span class="sxs-lookup"><span data-stu-id="d46f5-245">For example, if hello value is `"2013-15"` hello final request URL becomes `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span></span>  
  
<span data-ttu-id="d46f5-246">Daha fazla dönüştürme hello isteği olup olmadığını istenen, diğer [dönüştürme ilkelerini](api-management-transformation-policies.md#TransformationPolicies) kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-246">If further transformation of hello request is desired, other [Transformation policies](api-management-transformation-policies.md#TransformationPolicies) can be used.</span></span> <span data-ttu-id="d46f5-247">Merhaba istek bırakılıyor göre parametre yönlendirilen tooa sürüm belirli arka uç, hello Örneğin, tooremove hello sürüm sorgu [ayarlamak sorgu dizesi parametresi](api-management-transformation-policies.md#SetQueryStringParameter) İlkesi kullanılan tooremove hello şimdi yedek sürüm özniteliği olamaz.</span><span class="sxs-lookup"><span data-stu-id="d46f5-247">For example, tooremove hello version query parameter now that hello request is being routed tooa version specific backend, hello  [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policy can be used tooremove hello now redundant version attribute.</span></span>  
  
### <a name="example"></a><span data-ttu-id="d46f5-248">Örnek</span><span class="sxs-lookup"><span data-stu-id="d46f5-248">Example</span></span>  
  
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
<span data-ttu-id="d46f5-249">Bu örnek hello İlkesi yollar hello isteği tooa hizmet doku arka uç içinde hello UserID sorgu dizesi hello bölüm anahtarı olarak kullanma ve kullanma hello bölümünün birincil çoğaltmasını hello.</span><span class="sxs-lookup"><span data-stu-id="d46f5-249">In this example hello policy routes hello request tooa service fabric backend, using hello userId query string as hello partition key and using hello primary replica of hello partition.</span></span>  

### <a name="elements"></a><span data-ttu-id="d46f5-250">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="d46f5-250">Elements</span></span>  
  
|<span data-ttu-id="d46f5-251">Ad</span><span class="sxs-lookup"><span data-stu-id="d46f5-251">Name</span></span>|<span data-ttu-id="d46f5-252">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d46f5-252">Description</span></span>|<span data-ttu-id="d46f5-253">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d46f5-253">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d46f5-254">arka uç hizmet belirleme</span><span class="sxs-lookup"><span data-stu-id="d46f5-254">set-backend-service</span></span>|<span data-ttu-id="d46f5-255">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="d46f5-255">Root element.</span></span>|<span data-ttu-id="d46f5-256">Evet</span><span class="sxs-lookup"><span data-stu-id="d46f5-256">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d46f5-257">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="d46f5-257">Attributes</span></span>  
  
|<span data-ttu-id="d46f5-258">Ad</span><span class="sxs-lookup"><span data-stu-id="d46f5-258">Name</span></span>|<span data-ttu-id="d46f5-259">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d46f5-259">Description</span></span>|<span data-ttu-id="d46f5-260">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d46f5-260">Required</span></span>|<span data-ttu-id="d46f5-261">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="d46f5-261">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d46f5-262">Taban URL'si</span><span class="sxs-lookup"><span data-stu-id="d46f5-262">base-url</span></span>|<span data-ttu-id="d46f5-263">Yeni arka uç hizmeti temel URL'si.</span><span class="sxs-lookup"><span data-stu-id="d46f5-263">New backend service base URL.</span></span>|<span data-ttu-id="d46f5-264">Hayır</span><span class="sxs-lookup"><span data-stu-id="d46f5-264">No</span></span>|<span data-ttu-id="d46f5-265">Yok</span><span class="sxs-lookup"><span data-stu-id="d46f5-265">N/A</span></span>|  
|<span data-ttu-id="d46f5-266">arka uç kimliği</span><span class="sxs-lookup"><span data-stu-id="d46f5-266">backend-id</span></span>|<span data-ttu-id="d46f5-267">Merhaba arka uç tooroute tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="d46f5-267">Identifier of hello backend tooroute to.</span></span>|<span data-ttu-id="d46f5-268">Hayır</span><span class="sxs-lookup"><span data-stu-id="d46f5-268">No</span></span>|<span data-ttu-id="d46f5-269">Yok</span><span class="sxs-lookup"><span data-stu-id="d46f5-269">N/A</span></span>|  
|<span data-ttu-id="d46f5-270">BT bölüm anahtarı</span><span class="sxs-lookup"><span data-stu-id="d46f5-270">sf-partition-key</span></span>|<span data-ttu-id="d46f5-271">Yalnızca hello arka uç Service Fabric hizmeti ve 'arka uç-ID' kullanılarak belirtilen olduğunda geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-271">Only applicable when hello backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="d46f5-272">Tooresolve hello ad çözümleme hizmeti belirli bir bölümünden kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d46f5-272">Used tooresolve a specific partition from hello name resolution service.</span></span>|<span data-ttu-id="d46f5-273">Hayır</span><span class="sxs-lookup"><span data-stu-id="d46f5-273">No</span></span>|<span data-ttu-id="d46f5-274">Yok</span><span class="sxs-lookup"><span data-stu-id="d46f5-274">N/A</span></span>|  
|<span data-ttu-id="d46f5-275">BT çoğaltma türü</span><span class="sxs-lookup"><span data-stu-id="d46f5-275">sf-replica-type</span></span>|<span data-ttu-id="d46f5-276">Yalnızca hello arka uç Service Fabric hizmeti ve 'arka uç-ID' kullanılarak belirtilen olduğunda geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-276">Only applicable when hello backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="d46f5-277">Bir bölümün toohello birincil veya ikincil çoğaltma Hello isteği görünmeliyse denetler.</span><span class="sxs-lookup"><span data-stu-id="d46f5-277">Controls if hello request should go toohello primary or secondary replica of a partition.</span></span> |<span data-ttu-id="d46f5-278">Hayır</span><span class="sxs-lookup"><span data-stu-id="d46f5-278">No</span></span>|<span data-ttu-id="d46f5-279">Yok</span><span class="sxs-lookup"><span data-stu-id="d46f5-279">N/A</span></span>|    
|<span data-ttu-id="d46f5-280">BT çözümleme durumu</span><span class="sxs-lookup"><span data-stu-id="d46f5-280">sf-resolve-condition</span></span>|<span data-ttu-id="d46f5-281">Yalnızca hello arka uç Service Fabric hizmeti olduğunda geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-281">Only applicable when hello backend is a Service Fabric service.</span></span> <span data-ttu-id="d46f5-282">Merhaba tooService doku arka uç çağırırsanız koşulu tanımlayan yeni bir çözümleme yinelenen toobe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-282">Condition identifying if hello call tooService Fabric backend has toobe repeated with new resolution.</span></span>|<span data-ttu-id="d46f5-283">Hayır</span><span class="sxs-lookup"><span data-stu-id="d46f5-283">No</span></span>|<span data-ttu-id="d46f5-284">Yok</span><span class="sxs-lookup"><span data-stu-id="d46f5-284">N/A</span></span>|    
|<span data-ttu-id="d46f5-285">BT hizmet örneği adı</span><span class="sxs-lookup"><span data-stu-id="d46f5-285">sf-service-instance-name</span></span>|<span data-ttu-id="d46f5-286">Yalnızca hello arka uç Service Fabric hizmeti olduğunda geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-286">Only applicable when hello backend is a Service Fabric service.</span></span> <span data-ttu-id="d46f5-287">Toochange çalışma zamanında hizmet örnekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="d46f5-287">Allows toochange service instances at runtime.</span></span> |<span data-ttu-id="d46f5-288">Hayır</span><span class="sxs-lookup"><span data-stu-id="d46f5-288">No</span></span>|<span data-ttu-id="d46f5-289">Yok</span><span class="sxs-lookup"><span data-stu-id="d46f5-289">N/A</span></span>|    

### <a name="usage"></a><span data-ttu-id="d46f5-290">Kullanım</span><span class="sxs-lookup"><span data-stu-id="d46f5-290">Usage</span></span>  
 <span data-ttu-id="d46f5-291">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d46f5-291">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d46f5-292">**İlke bölümleri:** gelen, arka uç</span><span class="sxs-lookup"><span data-stu-id="d46f5-292">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="d46f5-293">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="d46f5-293">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d46f5-294"><a name="SetBody"></a>Set gövdesi</span><span class="sxs-lookup"><span data-stu-id="d46f5-294"><a name="SetBody"></a> Set body</span></span>  
 <span data-ttu-id="d46f5-295">Kullanım hello `set-body` gelen ve giden istekleri için ilke tooset hello ileti gövdesi.</span><span class="sxs-lookup"><span data-stu-id="d46f5-295">Use hello `set-body` policy tooset hello message body for incoming and outgoing requests.</span></span> <span data-ttu-id="d46f5-296">tooaccess hello hello kullanabileceğiniz ileti gövdesi `context.Request.Body` özelliği veya hello `context.Response.Body`hello İlkesi hello olmasına bağlı olarak gelen veya giden bölümü.</span><span class="sxs-lookup"><span data-stu-id="d46f5-296">tooaccess hello message body you can use hello `context.Request.Body` property or hello `context.Response.Body`, depending on whether hello policy is in hello inbound or outbound section.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="d46f5-297">Siz eriştiğinizde, varsayılan ileti gövdesi kullanarak hello unutmayın `context.Request.Body` veya `context.Response.Body`, gövde kaybolur ve geri hello ifadesinde hello gövde döndürerek ayarlanmalıdır hello özgün ileti.</span><span class="sxs-lookup"><span data-stu-id="d46f5-297">Note that by default when you access hello message body using `context.Request.Body` or `context.Response.Body`, hello original message body is lost and must be set by returning hello body back in hello expression.</span></span> <span data-ttu-id="d46f5-298">toopreserve hello gövdesi içeriği ayarlamak hello `preserveContent` parametresi çok`true` selamlama iletisine erişirken.</span><span class="sxs-lookup"><span data-stu-id="d46f5-298">toopreserve hello body content, set hello `preserveContent` parameter too`true` when accessing hello message.</span></span> <span data-ttu-id="d46f5-299">Varsa `preserveContent` çok ayarlanır`true` ve hello döndürülen gövde kullanılır farklı gövde hello ifadeyle döndürülür.</span><span class="sxs-lookup"><span data-stu-id="d46f5-299">If `preserveContent` is set too`true` and a different body is returned by hello expression, hello returned body is used.</span></span>  
>   
>  <span data-ttu-id="d46f5-300">Lütfen dikkat edilecek noktalar hello kullanırken aşağıdaki hello Not `set-body` ilkesi.</span><span class="sxs-lookup"><span data-stu-id="d46f5-300">Please note hello following considerations when using hello `set-body` policy.</span></span>  
>   
>  -   <span data-ttu-id="d46f5-301">Merhaba kullanıyorsanız `set-body` İlkesi tooreturn tooset gerekmez yeni veya güncelleştirilmiş bir gövde `preserveContent` çok`true` çünkü hello yeni gövdesi içeriği açıkça sağlamış olursunuz.</span><span class="sxs-lookup"><span data-stu-id="d46f5-301">If you are using hello `set-body` policy tooreturn a new or updated body you don't need tooset `preserveContent` too`true` because you are explicitly supplying hello new body contents.</span></span>  
> -   <span data-ttu-id="d46f5-302">Olmadığından yanıt henüz hello gelen ardışık düzeninde bir yanıt Merhaba içeriğine koruma doesn't make Sense.</span><span class="sxs-lookup"><span data-stu-id="d46f5-302">Preserving hello content of a response in hello inbound pipeline doesn't make sense because there is no response yet.</span></span>  
> -   <span data-ttu-id="d46f5-303">Merhaba istek zaten toohello arka uç bu noktada gönderildi çünkü hello giden ardışık düzeninde bir istek Merhaba içeriğine koruma doesn't make Sense.</span><span class="sxs-lookup"><span data-stu-id="d46f5-303">Preserving hello content of a request in hello outbound pipeline doesn't make sense because hello request has already been sent toohello backend at this point.</span></span>  
> -   <span data-ttu-id="d46f5-304">Örneğin ileti gövdesi yok olduğunda bu ilkeyi kullandıysanız, gelen bir GET içinde bir özel durum oluşur.</span><span class="sxs-lookup"><span data-stu-id="d46f5-304">If this policy is used when there is no message body, for example in an inbound GET, an exception is thrown.</span></span>  
  
 <span data-ttu-id="d46f5-305">Merhaba daha fazla bilgi için bkz: `context.Request.Body`, `context.Response.Body`ve hello `IMessage` hello bölümlerde [bağlamının](api-management-policy-expressions.md#ContextVariables) tablo.</span><span class="sxs-lookup"><span data-stu-id="d46f5-305">For more information, see hello `context.Request.Body`, `context.Response.Body`, and hello `IMessage` sections in hello [Context variable](api-management-policy-expressions.md#ContextVariables) table.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d46f5-306">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="d46f5-306">Policy statement</span></span>  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a><span data-ttu-id="d46f5-307">Örnekler</span><span class="sxs-lookup"><span data-stu-id="d46f5-307">Examples</span></span>  
  
#### <a name="literal-text-example"></a><span data-ttu-id="d46f5-308">Değişmez değer metni örneği</span><span class="sxs-lookup"><span data-stu-id="d46f5-308">Literal text example</span></span>  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-string-note-that-we-are-preserving-hello-original-request-body-so-that-we-can-access-it-later-in-hello-pipeline"></a><span data-ttu-id="d46f5-309">Örnek, dize olarak Hello gövdesi erişme.</span><span class="sxs-lookup"><span data-stu-id="d46f5-309">Example accessing hello body as a string.</span></span> <span data-ttu-id="d46f5-310">Biz bunu daha sonra hello ardışık düzeninde erişebilmesi için biz hello özgün istek gövdesi koruma olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d46f5-310">Note that we are preserving hello original request body so that we can access it later in hello pipeline.</span></span>
  
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
  
#### <a name="example-accessing-hello-body-as-a-jobject-note-that-since-we-are-not-reserving-hello-original-request-body-accesing-it-later-in-hello-pipeline-will-result-in-an-exception"></a><span data-ttu-id="d46f5-311">Örnek Hello gövdesi bir JObject olarak erişme.</span><span class="sxs-lookup"><span data-stu-id="d46f5-311">Example accessing hello body as a JObject.</span></span> <span data-ttu-id="d46f5-312">Biz hello özgün istek gövdesi, bunu daha sonra hello ardışık düzeninde bir özel durumla sonuçlanır belirtilmemelidir ayırma değil bu yana unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d46f5-312">Note that since we are not reserving hello original request body, accesing it later in hello pipeline will result in an exception.</span></span>  
  
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
  
#### <a name="filter-response-based-on-product"></a><span data-ttu-id="d46f5-313">Ürüne göre filtre yanıtı</span><span class="sxs-lookup"><span data-stu-id="d46f5-313">Filter response based on product</span></span>  
 <span data-ttu-id="d46f5-314">Bu örnek nasıl hello yanıttan veri öğeleri kaldırarak tooperform içerik filtreleme hello arka uç hizmetinden hello kullanırken alınan gösterir `Starter` ürün.</span><span class="sxs-lookup"><span data-stu-id="d46f5-314">This example shows how tooperform content filtering by removing data elements from hello response received from hello backend service when using hello `Starter` product.</span></span> <span data-ttu-id="d46f5-315">Yapılandırma ve bu ilkeyi kullanan bir örnek için bkz: [bulut kapak bölüm 177: daha Vlad Vinogradsky ile yönetim özelliklerini API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) ve too34:30 ileri sarma.</span><span class="sxs-lookup"><span data-stu-id="d46f5-315">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too34:30.</span></span> <span data-ttu-id="d46f5-316">Genel bir bakış 31:50 toosee Başlat [koyu Sky tahmin API hello](https://developer.forecast.io/) bu tanıtım için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d46f5-316">Start  at 31:50 toosee an overview of [hello Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
```xml  
<!-- Copy this snippet into hello outbound section tooremove a number of data elements from hello response received from hello backend service based on hello name of hello api product -->  
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

### <a name="using-liquid-templates-with-set-body"></a><span data-ttu-id="d46f5-317">Set gövde ile sıvı şablonlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="d46f5-317">Using Liquid templates with set body</span></span> 
<span data-ttu-id="d46f5-318">Merhaba `set-body` İlkesi, yapılandırılmış toouse hello olabilir [sıvı](https://shopify.github.io/liquid/basics/introduction/) şablon dili tootransfom hello gövdesi bir istek veya yanıt.</span><span class="sxs-lookup"><span data-stu-id="d46f5-318">hello `set-body` policy can be configured toouse hello [Liquid](https://shopify.github.io/liquid/basics/introduction/) templating language tootransfom hello body of a request or response.</span></span> <span data-ttu-id="d46f5-319">Bu iletinin toocompletely yeniden şekillendirme hello biçimi gerekiyorsa çok etkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-319">This can be very effective if you need toocompletely reshape hello format of your message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d46f5-320">hello kullanılan sıvı uyarlamasını hello `set-body` ilke ', C# modu' yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="d46f5-320">hello implementation of Liquid used in hello `set-body` policy is configured in 'C# mode'.</span></span> <span data-ttu-id="d46f5-321">Bu filtreleme gibi şeyler yaparken özellikle önemlidir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-321">This is particularly important when doing things such as filtering.</span></span> <span data-ttu-id="d46f5-322">Örnek olarak, bir tarih filtresi kullanarak Pascal hello kullanılmasını gerektiren büyük/küçük harf ve C# tarih biçimlendirme örn:</span><span class="sxs-lookup"><span data-stu-id="d46f5-322">As an example, using a date filter requires hello use of Pascal casing and C# date formatting e.g.:</span></span>
>
> <span data-ttu-id="d46f5-323">{{body.foo.startDateTime| Tarih: "yyyyMMddTHH:mm:ddZ"}}</span><span class="sxs-lookup"><span data-stu-id="d46f5-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d46f5-324">Hello sıvı şablonu kullanarak sipariş toocorrectly bağlama tooan XML metninde kullanmak bir `set-header` İlkesi tooset Content-Type tooeither uygulama/xml, text/xml (veya tüm ile biten türü + xml); JSON gövdesi için uygulama/json, text/json (veya tüm türü bitiş olmalıdır ile + json).</span><span class="sxs-lookup"><span data-stu-id="d46f5-324">In order toocorrectly bind tooan XML body using hello Liquid template, use a `set-header` policy tooset Content-Type tooeither application/xml, text/xml (or any type ending with +xml); for a JSON body, it must be application/json, text/json (or any type ending with +json).</span></span>

#### <a name="convert-json-toosoap-using-a-liquid-template"></a><span data-ttu-id="d46f5-325">Sıvı bir şablon kullanarak JSON tooSOAP Dönüştür</span><span class="sxs-lookup"><span data-stu-id="d46f5-325">Convert JSON tooSOAP using a Liquid template</span></span>
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

#### <a name="tranform-json-using-a-liquid-template"></a><span data-ttu-id="d46f5-326">Dönüşüm sıvı bir şablon kullanarak JSON</span><span class="sxs-lookup"><span data-stu-id="d46f5-326">Tranform JSON using a Liquid template</span></span>
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a><span data-ttu-id="d46f5-327">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="d46f5-327">Elements</span></span>  
  
|<span data-ttu-id="d46f5-328">Ad</span><span class="sxs-lookup"><span data-stu-id="d46f5-328">Name</span></span>|<span data-ttu-id="d46f5-329">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d46f5-329">Description</span></span>|<span data-ttu-id="d46f5-330">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d46f5-330">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d46f5-331">set-gövdesi</span><span class="sxs-lookup"><span data-stu-id="d46f5-331">set-body</span></span>|<span data-ttu-id="d46f5-332">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="d46f5-332">Root element.</span></span> <span data-ttu-id="d46f5-333">Merhaba gövde metin ya da body döndüren bir ifade içeriyor.</span><span class="sxs-lookup"><span data-stu-id="d46f5-333">Contains hello body text or an expressions that returns a body.</span></span>|<span data-ttu-id="d46f5-334">Evet</span><span class="sxs-lookup"><span data-stu-id="d46f5-334">Yes</span></span>|  

### <a name="properties"></a><span data-ttu-id="d46f5-335">Özellikler</span><span class="sxs-lookup"><span data-stu-id="d46f5-335">Properties</span></span>  
  
|<span data-ttu-id="d46f5-336">Ad</span><span class="sxs-lookup"><span data-stu-id="d46f5-336">Name</span></span>|<span data-ttu-id="d46f5-337">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d46f5-337">Description</span></span>|<span data-ttu-id="d46f5-338">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d46f5-338">Required</span></span>|<span data-ttu-id="d46f5-339">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="d46f5-339">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d46f5-340">şablon</span><span class="sxs-lookup"><span data-stu-id="d46f5-340">template</span></span>|<span data-ttu-id="d46f5-341">Gövde ilkesini ayarlama hello kullanılan toochange hello şablon oluşturma modunda çalıştırmak.</span><span class="sxs-lookup"><span data-stu-id="d46f5-341">Used toochange hello templating mode that hello set body policy will run in.</span></span> <span data-ttu-id="d46f5-342">Şu anda yalnızca desteklenen hello değeri şudur:</span><span class="sxs-lookup"><span data-stu-id="d46f5-342">Currently hello only supported value is:</span></span><br /><br /><span data-ttu-id="d46f5-343">-Sıvı - hello gövde ilkesini ayarlama hello sıvı şablon altyapısı kullanır</span><span class="sxs-lookup"><span data-stu-id="d46f5-343">- liquid - hello set body policy will use hello liquid templating engine</span></span> |<span data-ttu-id="d46f5-344">Hayır</span><span class="sxs-lookup"><span data-stu-id="d46f5-344">No</span></span>|<span data-ttu-id="d46f5-345">Sıvı</span><span class="sxs-lookup"><span data-stu-id="d46f5-345">liquid</span></span>|  

<span data-ttu-id="d46f5-346">Hello istek ve yanıt bilgilerine erişmek için hello sıvı şablonu tooa bağlam nesnesi aşağıdaki özelliklere hello ile bağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d46f5-346">For accessing information about hello request and response, hello Liquid template can bind tooa context object with hello following properties:</span></span> <br />
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



### <a name="usage"></a><span data-ttu-id="d46f5-347">Kullanım</span><span class="sxs-lookup"><span data-stu-id="d46f5-347">Usage</span></span>  
 <span data-ttu-id="d46f5-348">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d46f5-348">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d46f5-349">**İlke bölümleri:** gelen, giden arka uç</span><span class="sxs-lookup"><span data-stu-id="d46f5-349">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="d46f5-350">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="d46f5-350">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d46f5-351"><a name="SetHTTPheader"></a>HTTP üstbilgisi kümesi</span><span class="sxs-lookup"><span data-stu-id="d46f5-351"><a name="SetHTTPheader"></a> Set HTTP header</span></span>  
 <span data-ttu-id="d46f5-352">Merhaba `set-header` ilke değeri tooan varolan yanıt ve/veya istek üstbilgisi atar veya yeni bir yanıt ve/veya istek üstbilgisi ekler.</span><span class="sxs-lookup"><span data-stu-id="d46f5-352">hello `set-header` policy assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
 <span data-ttu-id="d46f5-353">HTTP üstbilgilerin listesi HTTP iletisine ekler.</span><span class="sxs-lookup"><span data-stu-id="d46f5-353">Inserts a list of HTTP headers into an HTTP message.</span></span> <span data-ttu-id="d46f5-354">Bir gelen ardışık düzeninde yerleştirildiğinde, bu ilkeyi toohello hedef hizmet geçirilen hello isteği hello HTTP üstbilgilerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d46f5-354">When placed in an inbound pipeline, this policy sets hello HTTP headers for hello request being passed toohello target service.</span></span> <span data-ttu-id="d46f5-355">Giden ardışık düzeninde yerleştirildiğinde, bu ilkeyi toohello ağ geçidi istemci gönderilen hello yanıt hello HTTP üstbilgilerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d46f5-355">When placed in an outbound pipeline, this policy sets hello HTTP headers for hello response being sent toohello gateway’s client.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d46f5-356">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="d46f5-356">Policy statement</span></span>  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with hello same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a><span data-ttu-id="d46f5-357">Örnekler</span><span class="sxs-lookup"><span data-stu-id="d46f5-357">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="d46f5-358">Örnek</span><span class="sxs-lookup"><span data-stu-id="d46f5-358">Example</span></span>  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a><span data-ttu-id="d46f5-359">Bağlam bilgileri toohello arka uç hizmeti ilet</span><span class="sxs-lookup"><span data-stu-id="d46f5-359">Forward context information toohello backend service</span></span>  
 <span data-ttu-id="d46f5-360">Bu örnek, tooapply İlkesi hello API düzey toosupply bağlam bilgileri toohello arka uç hizmetini nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-360">This example shows how tooapply policy at hello API level toosupply context information toohello backend service.</span></span> <span data-ttu-id="d46f5-361">Yapılandırma ve bu ilkeyi kullanan bir örnek için bkz: [bulut kapak bölüm 177: daha Vlad Vinogradsky ile yönetim özelliklerini API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) ve too10:30 ileri sarma.</span><span class="sxs-lookup"><span data-stu-id="d46f5-361">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too10:30.</span></span> <span data-ttu-id="d46f5-362">12:10 İşte hello İlkesi görebileceğiniz bir işlem hello Geliştirici Portalı'nda arama demo yoktur.</span><span class="sxs-lookup"><span data-stu-id="d46f5-362">At 12:10 there is a demo of calling an operation in hello developer portal where you can see hello policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward some context information, user id and hello region hello gateway is hosted in, toohello backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 <span data-ttu-id="d46f5-363">Daha fazla bilgi için bkz: [ilke ifadelerini](api-management-policy-expressions.md) ve [bağlamının](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="d46f5-363">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="d46f5-364">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="d46f5-364">Elements</span></span>  
  
|<span data-ttu-id="d46f5-365">Ad</span><span class="sxs-lookup"><span data-stu-id="d46f5-365">Name</span></span>|<span data-ttu-id="d46f5-366">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d46f5-366">Description</span></span>|<span data-ttu-id="d46f5-367">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d46f5-367">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d46f5-368">set üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="d46f5-368">set-header</span></span>|<span data-ttu-id="d46f5-369">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="d46f5-369">Root element.</span></span>|<span data-ttu-id="d46f5-370">Evet</span><span class="sxs-lookup"><span data-stu-id="d46f5-370">Yes</span></span>|  
|<span data-ttu-id="d46f5-371">değer</span><span class="sxs-lookup"><span data-stu-id="d46f5-371">value</span></span>|<span data-ttu-id="d46f5-372">Merhaba üstbilgi toobe kümesi Hello değerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-372">Specifies hello value of hello header toobe set.</span></span> <span data-ttu-id="d46f5-373">Merhaba ile birden çok üst bilgileri için aynı adı ekle ek `value` öğeleri.</span><span class="sxs-lookup"><span data-stu-id="d46f5-373">For multiple headers with hello same name add additional `value` elements.</span></span>|<span data-ttu-id="d46f5-374">Evet</span><span class="sxs-lookup"><span data-stu-id="d46f5-374">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="d46f5-375">Özellikler</span><span class="sxs-lookup"><span data-stu-id="d46f5-375">Properties</span></span>  
  
|<span data-ttu-id="d46f5-376">Ad</span><span class="sxs-lookup"><span data-stu-id="d46f5-376">Name</span></span>|<span data-ttu-id="d46f5-377">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d46f5-377">Description</span></span>|<span data-ttu-id="d46f5-378">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d46f5-378">Required</span></span>|<span data-ttu-id="d46f5-379">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="d46f5-379">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d46f5-380">Mevcut eylem</span><span class="sxs-lookup"><span data-stu-id="d46f5-380">exists-action</span></span>|<span data-ttu-id="d46f5-381">Merhaba üstbilgi zaten belirtildiğinde hangi eylemini tootake belirtir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-381">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="d46f5-382">Bu öznitelik değerlerini aşağıdaki hello birine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d46f5-382">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="d46f5-383">-değiştirir hello hello varolan üstbilgisinin değerini geçersiz kıl -.</span><span class="sxs-lookup"><span data-stu-id="d46f5-383">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="d46f5-384">-skip - hello varolan üstbilgi değeri değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="d46f5-384">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="d46f5-385">-Ekle - hello değeri toohello varolan üstbilgi değeri ekler.</span><span class="sxs-lookup"><span data-stu-id="d46f5-385">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="d46f5-386">-delete - hello üstbilgisini hello isteğinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="d46f5-386">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="d46f5-387">Ayarlandığında çok`override` birden çok girişi kaydetme; hello ile aynı sonuçları (birden çok kez listelenir) kümesi according tooall girdisi olan hello üstbilgisinde adı yalnızca listelenen değerler hello sonucunda ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="d46f5-387">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="d46f5-388">Hayır</span><span class="sxs-lookup"><span data-stu-id="d46f5-388">No</span></span>|<span data-ttu-id="d46f5-389">geçersiz kılma</span><span class="sxs-lookup"><span data-stu-id="d46f5-389">override</span></span>|  
|<span data-ttu-id="d46f5-390">ad</span><span class="sxs-lookup"><span data-stu-id="d46f5-390">name</span></span>|<span data-ttu-id="d46f5-391">Merhaba üstbilgi toobe kümesinin adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-391">Specifies name of hello header toobe set.</span></span>|<span data-ttu-id="d46f5-392">Evet</span><span class="sxs-lookup"><span data-stu-id="d46f5-392">Yes</span></span>|<span data-ttu-id="d46f5-393">Yok</span><span class="sxs-lookup"><span data-stu-id="d46f5-393">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d46f5-394">Kullanım</span><span class="sxs-lookup"><span data-stu-id="d46f5-394">Usage</span></span>  
 <span data-ttu-id="d46f5-395">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d46f5-395">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d46f5-396">**İlke bölümleri:** gelen, giden arka uç, hata</span><span class="sxs-lookup"><span data-stu-id="d46f5-396">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="d46f5-397">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="d46f5-397">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d46f5-398"><a name="SetQueryStringParameter"></a>Set sorgu dizesi parametresi</span><span class="sxs-lookup"><span data-stu-id="d46f5-398"><a name="SetQueryStringParameter"></a> Set query string parameter</span></span>  
 <span data-ttu-id="d46f5-399">Merhaba `set-query-parameter` ilkesi ekler, değiştirir değeri, veya silme isteği sorgu dizesi parametresi.</span><span class="sxs-lookup"><span data-stu-id="d46f5-399">hello `set-query-parameter` policy adds, replaces value of, or deletes request query string parameter.</span></span> <span data-ttu-id="d46f5-400">Kullanılan toopass isteğe bağlı olan veya hiç hello istekte mevcut hello arka uç hizmeti tarafından beklenen sorgu parametreleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-400">Can be used toopass query parameters expected by hello backend service which are optional or never present in hello request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d46f5-401">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="d46f5-401">Policy statement</span></span>  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with hello same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a><span data-ttu-id="d46f5-402">Örnekler</span><span class="sxs-lookup"><span data-stu-id="d46f5-402">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="d46f5-403">Örnek</span><span class="sxs-lookup"><span data-stu-id="d46f5-403">Example</span></span>  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with hello same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a><span data-ttu-id="d46f5-404">Bağlam bilgileri toohello arka uç hizmeti ilet</span><span class="sxs-lookup"><span data-stu-id="d46f5-404">Forward context information toohello backend service</span></span>  
 <span data-ttu-id="d46f5-405">Bu örnek, tooapply İlkesi hello API düzey toosupply bağlam bilgileri toohello arka uç hizmetini nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-405">This example shows how tooapply policy at hello API level toosupply context information toohello backend service.</span></span> <span data-ttu-id="d46f5-406">Yapılandırma ve bu ilkeyi kullanan bir örnek için bkz: [bulut kapak bölüm 177: daha Vlad Vinogradsky ile yönetim özelliklerini API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) ve too10:30 ileri sarma.</span><span class="sxs-lookup"><span data-stu-id="d46f5-406">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too10:30.</span></span> <span data-ttu-id="d46f5-407">12:10 İşte hello İlkesi görebileceğiniz bir işlem hello Geliştirici Portalı'nda arama demo yoktur.</span><span class="sxs-lookup"><span data-stu-id="d46f5-407">At 12:10 there is a demo of calling an operation in hello developer portal where you can see hello policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward a piece of context, product name in this example, toohello backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 <span data-ttu-id="d46f5-408">Daha fazla bilgi için bkz: [ilke ifadelerini](api-management-policy-expressions.md) ve [bağlamının](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="d46f5-408">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="d46f5-409">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="d46f5-409">Elements</span></span>  
  
|<span data-ttu-id="d46f5-410">Ad</span><span class="sxs-lookup"><span data-stu-id="d46f5-410">Name</span></span>|<span data-ttu-id="d46f5-411">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d46f5-411">Description</span></span>|<span data-ttu-id="d46f5-412">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d46f5-412">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d46f5-413">kümesi sorgu parametresi</span><span class="sxs-lookup"><span data-stu-id="d46f5-413">set-query-parameter</span></span>|<span data-ttu-id="d46f5-414">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="d46f5-414">Root element.</span></span>|<span data-ttu-id="d46f5-415">Evet</span><span class="sxs-lookup"><span data-stu-id="d46f5-415">Yes</span></span>|  
|<span data-ttu-id="d46f5-416">değer</span><span class="sxs-lookup"><span data-stu-id="d46f5-416">value</span></span>|<span data-ttu-id="d46f5-417">Merhaba sorgu parametresi toobe kümesi Hello değerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-417">Specifies hello value of hello query parameter toobe set.</span></span> <span data-ttu-id="d46f5-418">Merhaba ile birden çok sorgu parametreleri için aynı adı ekle ek `value` öğeleri.</span><span class="sxs-lookup"><span data-stu-id="d46f5-418">For multiple query parameters with hello same name add additional `value` elements.</span></span>|<span data-ttu-id="d46f5-419">Evet</span><span class="sxs-lookup"><span data-stu-id="d46f5-419">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="d46f5-420">Özellikler</span><span class="sxs-lookup"><span data-stu-id="d46f5-420">Properties</span></span>  
  
|<span data-ttu-id="d46f5-421">Ad</span><span class="sxs-lookup"><span data-stu-id="d46f5-421">Name</span></span>|<span data-ttu-id="d46f5-422">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d46f5-422">Description</span></span>|<span data-ttu-id="d46f5-423">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d46f5-423">Required</span></span>|<span data-ttu-id="d46f5-424">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="d46f5-424">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d46f5-425">Mevcut eylem</span><span class="sxs-lookup"><span data-stu-id="d46f5-425">exists-action</span></span>|<span data-ttu-id="d46f5-426">Merhaba sorgu parametresi zaten belirtildiğinde hangi eylemini tootake belirtir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-426">Specifies what action tootake when hello query parameter is already specified.</span></span> <span data-ttu-id="d46f5-427">Bu öznitelik değerlerini aşağıdaki hello birine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d46f5-427">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="d46f5-428">-değiştirir hello hello varolan parametresinin değerini geçersiz kıl -.</span><span class="sxs-lookup"><span data-stu-id="d46f5-428">-   override - replaces hello value of hello existing parameter.</span></span><br /><span data-ttu-id="d46f5-429">-skip - hello varolan sorgusu parametre değeri değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="d46f5-429">-   skip - does not replace hello existing query parameter value.</span></span><br /><span data-ttu-id="d46f5-430">-Ekle - hello değeri toohello varolan sorgusu parametre değeri ekler.</span><span class="sxs-lookup"><span data-stu-id="d46f5-430">-   append - appends hello value toohello existing query parameter value.</span></span><br /><span data-ttu-id="d46f5-431">-delete - hello sorgu parametresi hello isteğinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="d46f5-431">-   delete - removes hello query parameter from hello request.</span></span><br /><br /> <span data-ttu-id="d46f5-432">Ayarlandığında çok`override` birden çok girişi kaydetme; hello ile aynı (birden çok kez listelenir) kümesi according tooall girdisi olan hello sorgu parametresi sonuçlarında adı yalnızca listelenen değerler hello sonucunda ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="d46f5-432">When set too`override` enlisting multiple entries with hello same name results in hello query parameter being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="d46f5-433">Hayır</span><span class="sxs-lookup"><span data-stu-id="d46f5-433">No</span></span>|<span data-ttu-id="d46f5-434">geçersiz kılma</span><span class="sxs-lookup"><span data-stu-id="d46f5-434">override</span></span>|  
|<span data-ttu-id="d46f5-435">ad</span><span class="sxs-lookup"><span data-stu-id="d46f5-435">name</span></span>|<span data-ttu-id="d46f5-436">Merhaba sorgu parametresi toobe kümesinin adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-436">Specifies name of hello query parameter toobe set.</span></span>|<span data-ttu-id="d46f5-437">Evet</span><span class="sxs-lookup"><span data-stu-id="d46f5-437">Yes</span></span>|<span data-ttu-id="d46f5-438">Yok</span><span class="sxs-lookup"><span data-stu-id="d46f5-438">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d46f5-439">Kullanım</span><span class="sxs-lookup"><span data-stu-id="d46f5-439">Usage</span></span>  
 <span data-ttu-id="d46f5-440">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d46f5-440">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d46f5-441">**İlke bölümleri:** gelen, arka uç</span><span class="sxs-lookup"><span data-stu-id="d46f5-441">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="d46f5-442">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="d46f5-442">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d46f5-443"><a name="RewriteURL"></a>URL yeniden yazma</span><span class="sxs-lookup"><span data-stu-id="d46f5-443"><a name="RewriteURL"></a> Rewrite URL</span></span>  
 <span data-ttu-id="d46f5-444">Merhaba `rewrite-uri` ilkeyi dönüştürür istek URL'si hello web hizmeti tarafından beklenen genel form toohello formundan hello aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="d46f5-444">hello `rewrite-uri` policy converts a request URL from its public form toohello form expected by hello web service, as shown in hello following example.</span></span>  
  
-   <span data-ttu-id="d46f5-445">Ortak URL-`http://api.example.com/storenumber/ordernumber`</span><span class="sxs-lookup"><span data-stu-id="d46f5-445">Public URL - `http://api.example.com/storenumber/ordernumber`</span></span>  
  
-   <span data-ttu-id="d46f5-446">İstek URL-`http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span><span class="sxs-lookup"><span data-stu-id="d46f5-446">Request URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span></span>  
  
 <span data-ttu-id="d46f5-447">Bu ilke, İnsan ve/veya tarayıcı kolay URL hello web hizmeti tarafından beklenen hello URL biçimine dönüştürülmesi gereken olduğunda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d46f5-447">This policy can be used when a human and/or browser-friendly URL should be transformed into hello URL format expected by hello web service.</span></span> <span data-ttu-id="d46f5-448">Bu ilke, yalnızca temiz URL'leri, RESTful URL'leri, kullanıcı dostu URL'leri veya bir sorgu dizesi içermiyor ve bunun yerine yalnızca hello hello yolunu içeren zamanıyla ilgili yapısal URL'leri SEO dostu URL'leri gibi alternatif bir URL biçimi gösterme uygulanır toobe gerekir Kaynak (sonra hello şema ve hello yetkili).</span><span class="sxs-lookup"><span data-stu-id="d46f5-448">This policy only needs toobe applied when exposing an alternative URL format, such as clean URLs, RESTful URLs, user-friendly URLs or SEO-friendly URLs that are purely structural URLs that do not contain a query string and instead contain only hello path of hello resource (after hello scheme and hello authority).</span></span> <span data-ttu-id="d46f5-449">Bu genellikle estetik, kullanılabilirlik veya arama motoru iyileştirmesi (SEO) amacıyla yapılır.</span><span class="sxs-lookup"><span data-stu-id="d46f5-449">This is often done for aesthetic, usability, or search engine optimization (SEO) purposes.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="d46f5-450">Sorgu dizesi parametreleri hello İlkesi'ni kullanarak yalnızca ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d46f5-450">You can only add query string parameters using hello policy.</span></span> <span data-ttu-id="d46f5-451">Ek şablon yolu hello parametrelerinde URL yeniden yazma ekleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="d46f5-451">You cannot add extra template path parameters in hello rewrite URL.</span></span>  

### <a name="policy-statement"></a><span data-ttu-id="d46f5-452">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="d46f5-452">Policy statement</span></span>  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a><span data-ttu-id="d46f5-453">Örnek</span><span class="sxs-lookup"><span data-stu-id="d46f5-453">Example</span></span>  
  
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
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
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
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
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

### <a name="elements"></a><span data-ttu-id="d46f5-454">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="d46f5-454">Elements</span></span>  
  
|<span data-ttu-id="d46f5-455">Ad</span><span class="sxs-lookup"><span data-stu-id="d46f5-455">Name</span></span>|<span data-ttu-id="d46f5-456">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d46f5-456">Description</span></span>|<span data-ttu-id="d46f5-457">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d46f5-457">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d46f5-458">yeniden yazma URI'sı</span><span class="sxs-lookup"><span data-stu-id="d46f5-458">rewrite-uri</span></span>|<span data-ttu-id="d46f5-459">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="d46f5-459">Root element.</span></span>|<span data-ttu-id="d46f5-460">Evet</span><span class="sxs-lookup"><span data-stu-id="d46f5-460">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d46f5-461">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="d46f5-461">Attributes</span></span>  
  
|<span data-ttu-id="d46f5-462">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="d46f5-462">Attribute</span></span>|<span data-ttu-id="d46f5-463">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d46f5-463">Description</span></span>|<span data-ttu-id="d46f5-464">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d46f5-464">Required</span></span>|<span data-ttu-id="d46f5-465">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="d46f5-465">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="d46f5-466">şablon</span><span class="sxs-lookup"><span data-stu-id="d46f5-466">template</span></span>|<span data-ttu-id="d46f5-467">herhangi bir sorgu dizesi parametre ile Merhaba gerçek web hizmeti URL'si.</span><span class="sxs-lookup"><span data-stu-id="d46f5-467">hello actual web service URL with any query string parameters.</span></span> <span data-ttu-id="d46f5-468">İfadeler kullanırken hello tam değeri bir ifade olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d46f5-468">When using expressions, hello whole value must be an expression.</span></span>|<span data-ttu-id="d46f5-469">Evet</span><span class="sxs-lookup"><span data-stu-id="d46f5-469">Yes</span></span>|<span data-ttu-id="d46f5-470">Yok</span><span class="sxs-lookup"><span data-stu-id="d46f5-470">N/A</span></span>|  
|<span data-ttu-id="d46f5-471">kopya eşleşmeyen-parametreleri</span><span class="sxs-lookup"><span data-stu-id="d46f5-471">copy-unmatched-params</span></span>|<span data-ttu-id="d46f5-472">Sorgu parametrelerini gelen istekteki hello hello özgün URL şablonunda mevcut değil hello tarafından tanımlanan toohello URL yeniden yazma şablon eklenip eklenmeyeceğini belirtir</span><span class="sxs-lookup"><span data-stu-id="d46f5-472">Specifies whether query parameters in hello incoming request not present in hello original URL template are added toohello URL defined by hello re-write template</span></span>|<span data-ttu-id="d46f5-473">Hayır</span><span class="sxs-lookup"><span data-stu-id="d46f5-473">No</span></span>|<span data-ttu-id="d46f5-474">TRUE</span><span class="sxs-lookup"><span data-stu-id="d46f5-474">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d46f5-475">Kullanım</span><span class="sxs-lookup"><span data-stu-id="d46f5-475">Usage</span></span>  
 <span data-ttu-id="d46f5-476">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d46f5-476">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d46f5-477">**İlke bölümleri:** gelen</span><span class="sxs-lookup"><span data-stu-id="d46f5-477">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="d46f5-478">**İlke kapsamları:** ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="d46f5-478">**Policy scopes:** product, API, operation</span></span>  
  
##  <span data-ttu-id="d46f5-479"><a name="XSLTransform"></a>XSLT kullanarak XML dönüştürme</span><span class="sxs-lookup"><span data-stu-id="d46f5-479"><a name="XSLTransform"></a> Transform XML using an XSLT</span></span>  
 <span data-ttu-id="d46f5-480">Merhaba `Transform XML using an XSLT` ilke bir XSL Dönüştürme tooXML hello istek veya yanıt gövdesi içinde uygulanır.</span><span class="sxs-lookup"><span data-stu-id="d46f5-480">hello `Transform XML using an XSLT` policy applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d46f5-481">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="d46f5-481">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="d46f5-482">Örnek</span><span class="sxs-lookup"><span data-stu-id="d46f5-482">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="d46f5-483">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="d46f5-483">Elements</span></span>  
  
|<span data-ttu-id="d46f5-484">Ad</span><span class="sxs-lookup"><span data-stu-id="d46f5-484">Name</span></span>|<span data-ttu-id="d46f5-485">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d46f5-485">Description</span></span>|<span data-ttu-id="d46f5-486">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d46f5-486">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d46f5-487">XSL Dönüştürme</span><span class="sxs-lookup"><span data-stu-id="d46f5-487">xsl-transform</span></span>|<span data-ttu-id="d46f5-488">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="d46f5-488">Root element.</span></span>|<span data-ttu-id="d46f5-489">Evet</span><span class="sxs-lookup"><span data-stu-id="d46f5-489">Yes</span></span>|  
|<span data-ttu-id="d46f5-490">Parametre</span><span class="sxs-lookup"><span data-stu-id="d46f5-490">parameter</span></span>|<span data-ttu-id="d46f5-491">Merhaba dönüşüm dosyasında kullanılan kullanılan toodefine değişkenler</span><span class="sxs-lookup"><span data-stu-id="d46f5-491">Used toodefine variables used in hello transform</span></span>|<span data-ttu-id="d46f5-492">Hayır</span><span class="sxs-lookup"><span data-stu-id="d46f5-492">No</span></span>|  
|<span data-ttu-id="d46f5-493">stylesheet</span><span class="sxs-lookup"><span data-stu-id="d46f5-493">xsl:stylesheet</span></span>|<span data-ttu-id="d46f5-494">Kök stil öğesi.</span><span class="sxs-lookup"><span data-stu-id="d46f5-494">Root stylesheet element.</span></span> <span data-ttu-id="d46f5-495">Tüm öğeleri ve özniteliklerinin içinde tanımlanan hello standarda [XSLT belirtimi](http://www.w3.org/TR/xslt)</span><span class="sxs-lookup"><span data-stu-id="d46f5-495">All elements and attributes defined within follow hello standard [XSLT specification](http://www.w3.org/TR/xslt)</span></span>|<span data-ttu-id="d46f5-496">Evet</span><span class="sxs-lookup"><span data-stu-id="d46f5-496">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d46f5-497">Kullanım</span><span class="sxs-lookup"><span data-stu-id="d46f5-497">Usage</span></span>  
 <span data-ttu-id="d46f5-498">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d46f5-498">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d46f5-499">**İlke bölümleri:** gelen, giden</span><span class="sxs-lookup"><span data-stu-id="d46f5-499">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="d46f5-500">**İlke kapsamları:** genel, ürün, API işlemi</span><span class="sxs-lookup"><span data-stu-id="d46f5-500">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="d46f5-501">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d46f5-501">Next steps</span></span>
<span data-ttu-id="d46f5-502">İlkeleriyle çalışma daha fazla bilgi için bkz: [API Management ilkeleri](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="d46f5-502">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
