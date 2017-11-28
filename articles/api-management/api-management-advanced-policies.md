---
title: "API Management ilkeleri Gelişmiş aaaAzure | Microsoft Docs"
description: "Azure API Management'te kullanıma ilkeleri Gelişmiş hello hakkında bilgi edinin."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 8a13348b-7856-428f-8e35-9e4273d94323
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 8245e7a4c9d432b7b4d362192e357829fcabad55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-advanced-policies"></a><span data-ttu-id="1f6a0-103">API Management ilkeleri Gelişmiş</span><span class="sxs-lookup"><span data-stu-id="1f6a0-103">API Management advanced policies</span></span>
<span data-ttu-id="1f6a0-104">Bu konuda API Management ilkelere hello için bir başvuru sağlar.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="1f6a0-105">Ekleme ve ilkeleri yapılandırma hakkında daha fazla bilgi için bkz: [API Management ilkeleri](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="1f6a0-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="1f6a0-106"><a name="AdvancedPolicies"></a>Gelişmiş ilkeleri</span><span class="sxs-lookup"><span data-stu-id="1f6a0-106"><a name="AdvancedPolicies"></a> Advanced policies</span></span>  
  
-   <span data-ttu-id="1f6a0-107">[Denetim akışı](api-management-advanced-policies.md#choose) - koşullu ilke deyimleri hello hello değerlendirme Boole sonuçlarına dayalı uygular [ifadeleri](api-management-policy-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="1f6a0-107">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on hello results of hello evaluation of Boolean [expressions](api-management-policy-expressions.md).</span></span>  
  
-   <span data-ttu-id="1f6a0-108">[İstek](#ForwardRequest) -hello isteği toohello arka uç hizmeti iletir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-108">[Forward request](#ForwardRequest) - Forwards hello request toohello backend service.</span></span>

-   <span data-ttu-id="1f6a0-109">[Eşzamanlılık sınırlamak](#LimitConcurrency) -engeller içine tarafından belirtilen istek sayısının aynı anda hello fazlasını yürütülmesini ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-109">[Limit concurrency](#LimitConcurrency) - Prevents enclosed policies from executing by more than hello specified number of requests at a time.</span></span>
  
-   <span data-ttu-id="1f6a0-110">[TooEvent Hub oturum](#log-to-eventhub) -hello gönderdiği iletileri belirtilen olay hub'ı Günlükçü varlık tarafından tanımlanan biçimi tooan.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-110">[Log tooEvent Hub](#log-to-eventhub) - Sends messages in hello specified format tooan Event Hub defined by a Logger entity.</span></span> 

-   <span data-ttu-id="1f6a0-111">[Yanıt mock](#mock-response) -iptalleri potansiyel satış, yürütme ve mocked bir yanıt döndürür doğrudan toohello çağıran.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-111">[Mock response](#mock-response) - Aborts pipeline execution and returns a mocked response directly toohello caller.</span></span>
  
-   <span data-ttu-id="1f6a0-112">[Yeniden deneme](#Retry) -hello yürütülmesi yeniden deneme içine ilke deyimleri varsa ve hello koşul yerine getirilene kadar.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-112">[Retry](#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="1f6a0-113">Yürütme yineleyin belirtilen zaman aralığı hello ve belirtilen toohello yeniden deneme sayısı.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-113">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>  
  
-   <span data-ttu-id="1f6a0-114">[Yanıt](#ReturnResponse) -iptalleri ardışık düzen yürütmesi ve döndürür hello belirtilen yanıt doğrudan toohello çağıran.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-114">[Return response](#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span> 
  
-   <span data-ttu-id="1f6a0-115">[Tek yönlü İsteği Gönder](#SendOneWayRequest) -bir istek toohello belirtilen URL için bir yanıt beklemeden gönderir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-115">[Send one way request](#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>  
  
-   <span data-ttu-id="1f6a0-116">[İsteği Gönder](#SendRequest) -bir istek toohello belirtilen URL gönderir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-116">[Send request](#SendRequest) - Sends a request toohello specified URL.</span></span>  

-   <span data-ttu-id="1f6a0-117">[HTTP proxy ayarlamak](#SetHttpProxy) -bir HTTP proxy üzerinden iletilen tooroute isteklere izin verir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-117">[Set HTTP proxy](#SetHttpProxy) - Allows you tooroute forwarded requests via an HTTP proxy.</span></span>  

-   <span data-ttu-id="1f6a0-118">[İstek yöntemini ayarla](#SetRequestMethod) -bir istek için toochange hello HTTP yöntemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-118">[Set request method](#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>  
  
-   <span data-ttu-id="1f6a0-119">[Durum kodu ayarlamak](#SetStatus) -değişiklikleri hello HTTP durum kodu toohello belirtilen değeri.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-119">[Set status code](#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>  
  
-   <span data-ttu-id="1f6a0-120">[Değişken Ayarla](api-management-advanced-policies.md#set-variable) -adlandırılmış bir değer devam [bağlamı](api-management-policy-expressions.md#ContextVariables) sonraki erişim için değişken.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-120">[Set variable](api-management-advanced-policies.md#set-variable) - Persists a value in a named [context](api-management-policy-expressions.md#ContextVariables) variable for later access.</span></span>  

-   <span data-ttu-id="1f6a0-121">[İzleme](#Trace) -hello bir dize ekler [API denetçisi](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) çıktı.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-121">[Trace](#Trace) - Adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
-   <span data-ttu-id="1f6a0-122">[Bekleyin](#Wait) -içine için bekleyeceği [gönderme isteği](api-management-advanced-policies.md#SendRequest), [değeri önbellekten alma](api-management-caching-policies.md#GetFromCacheByKey), veya [kontrol akışı](api-management-advanced-policies.md#choose) ilkeleri toocomplete devam etmeden önce.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-122">[Wait](#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies toocomplete before proceeding.</span></span>  
  
##  <span data-ttu-id="1f6a0-123"><a name="choose"></a>Denetim akışı</span><span class="sxs-lookup"><span data-stu-id="1f6a0-123"><a name="choose"></a> Control flow</span></span>  
 <span data-ttu-id="1f6a0-124">Merhaba `choose` ilke ifadeleri değerlendirme Boole ifadeleri, benzer tooan IF-then-else veya bir anahtar hello sonucunu temel alarak bir programlama dilinde oluşturmak iliştirilmiş ilke uygulanır.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-124">hello `choose` policy applies enclosed policy statements based on hello outcome of evaluation of Boolean expressions, similar tooan if-then-else or a switch construct in a programming language.</span></span>  
  
###  <span data-ttu-id="1f6a0-125"><a name="ChoosePolicyStatement"></a>İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-125"><a name="ChoosePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<choose>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <otherwise>   
        <!— one or more policy statements toobe applied if none of hello above conditions are true  -->  
</otherwise>   
</choose>  
```  
  
 <span data-ttu-id="1f6a0-126">Merhaba denetim akışı ilke en az birini içermelidir `<when/>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-126">hello control flow policy must contain at least one `<when/>` element.</span></span> <span data-ttu-id="1f6a0-127">Merhaba `<otherwise/>` öğesidir isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-127">hello `<otherwise/>` element is optional.</span></span> <span data-ttu-id="1f6a0-128">Koşulları `<when/>` öğeleri sırasına görünümlerini hello ilke içinde değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-128">Conditions in `<when/>` elements are evaluated in order of their appearance within hello policy.</span></span> <span data-ttu-id="1f6a0-129">İlke deyim Hello içinde ilk içine `<when/>` koşul özniteliği eşittir öğeyle `true` uygulanır.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-129">Policy statement(s) enclosed within hello first `<when/>` element with condition attribute equals `true` will be applied.</span></span> <span data-ttu-id="1f6a0-130">İçinde Hello içine ilkeleri `<otherwise/>` öğesi, varsa, tüm uygulanacak Merhaba, `<when/>` öğesi koşul öznitelikleri `false`.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-130">Policies enclosed within hello `<otherwise/>` element, if present, will be applied if all of hello `<when/>` element condition attributes are `false`.</span></span>  
  
### <a name="examples"></a><span data-ttu-id="1f6a0-131">Örnekler</span><span class="sxs-lookup"><span data-stu-id="1f6a0-131">Examples</span></span>  
  
####  <span data-ttu-id="1f6a0-132"><a name="ChooseExample"></a>Örnek</span><span class="sxs-lookup"><span data-stu-id="1f6a0-132"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="1f6a0-133">Merhaba aşağıdaki örnekte gösterilmiştir bir [değişken Ayarla](api-management-advanced-policies.md#set-variable) İlkesi ve iki denetim akışı ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-133">hello following example demonstrates a [set-variable](api-management-advanced-policies.md#set-variable) policy and two control flow policies.</span></span>  
  
 <span data-ttu-id="1f6a0-134">gelen bölüm hello ve oluşturur Hello değişken ilkesini ayarlama zamanı bir `isMobile` Boolean [bağlamı](api-management-policy-expressions.md#ContextVariables) tootrue hello ayarlanır değişkeni `User-Agent` istek üstbilgisi hello metni içerir `iPad` veya `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-134">hello set variable policy is in hello inbound section and creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set tootrue if hello `User-Agent` request header contains hello text `iPad` or `iPhone`.</span></span>  
  
 <span data-ttu-id="1f6a0-135">Merhaba ilk denetim akışı ilke konusu de gelen bölüm hello ve koşullu iki biri geçerlidir [ayarlamak sorgu dizesi parametresi](api-management-transformation-policies.md#SetQueryStringParameter) hello hello değerine bağlı olarak ilkeleri `isMobile` bağlamının.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-135">hello first control flow policy is also in hello inbound section, and conditionally applies one of two [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policies depending on hello value of hello `isMobile` context variable.</span></span>  
  
 <span data-ttu-id="1f6a0-136">Merhaba ikinci denetim akışı ilke hello giden bölümünde ve koşullu hello geçerlidir [Dönüştür XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) İlkesi zaman `isMobile` çok ayarlanır`true`.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-136">hello second control flow policy is in hello outbound section and conditionally applies hello [Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) policy when `isMobile` is set too`true`.</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <set-variable name="isMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
        <base />  
        <choose>  
            <when condition="@(context.Variables.GetValueOrDefault<bool>("isMobile"))">  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>true</value>  
                </set-query-parameter>  
            </when>  
            <otherwise>  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>false</value>  
                </set-query-parameter>  
            </otherwise>  
        </choose>  
    </inbound>  
    <outbound>  
        <base />  
        <choose>  
            <when condition="@(context.GetValueOrDefault<bool>("isMobile"))">  
                <xml-to-json kind="direct" apply="always" consider-accept-header="false"/>  
            </when>  
        </choose>  
    </outbound>  
</policies>  
```  
  
#### <a name="example"></a><span data-ttu-id="1f6a0-137">Örnek</span><span class="sxs-lookup"><span data-stu-id="1f6a0-137">Example</span></span>  
 <span data-ttu-id="1f6a0-138">Bu örnek nasıl hello yanıttan veri öğeleri kaldırarak tooperform içerik filtreleme hello arka uç hizmetinden hello kullanırken alınan gösterir `Starter` ürün.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-138">This example shows how tooperform content filtering by removing data elements from hello response received from hello backend service when using hello `Starter` product.</span></span> <span data-ttu-id="1f6a0-139">Yapılandırma ve bu ilkeyi kullanan bir örnek için bkz: [bulut kapak bölüm 177: daha Vlad Vinogradsky ile yönetim özelliklerini API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) ve too34:30 ileri sarma.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-139">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too34:30.</span></span> <span data-ttu-id="1f6a0-140">Genel bir bakış 31:50 toosee Başlat [koyu Sky tahmin API hello](https://developer.forecast.io/) bu tanıtım için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-140">Start  at 31:50 toosee an overview of [hello Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="1f6a0-141">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="1f6a0-141">Elements</span></span>  
  
|<span data-ttu-id="1f6a0-142">Öğesi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-142">Element</span></span>|<span data-ttu-id="1f6a0-143">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-143">Description</span></span>|<span data-ttu-id="1f6a0-144">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-144">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1f6a0-145">seçin</span><span class="sxs-lookup"><span data-stu-id="1f6a0-145">choose</span></span>|<span data-ttu-id="1f6a0-146">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-146">Root element.</span></span>|<span data-ttu-id="1f6a0-147">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-147">Yes</span></span>|  
|<span data-ttu-id="1f6a0-148">ne zaman</span><span class="sxs-lookup"><span data-stu-id="1f6a0-148">when</span></span>|<span data-ttu-id="1f6a0-149">Koşul toouse hello için hello `if` veya `ifelse` hello bölümlerini `choose` ilkesi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-149">hello condition toouse for hello `if` or `ifelse` parts of hello `choose` policy.</span></span> <span data-ttu-id="1f6a0-150">Merhaba, `choose` ilkesine sahip birden çok `when` bölümler, sıralı olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-150">If hello `choose` policy has multiple `when` sections, they are evaluated sequentially.</span></span> <span data-ttu-id="1f6a0-151">Bir kez hello `condition` olduğunda öğesi çok değerlendirir`true`, daha fazla `when` koşullar değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-151">Once hello `condition` of a when element evaluates too`true`, no further `when` conditions are evaluated.</span></span>|<span data-ttu-id="1f6a0-152">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-152">Yes</span></span>|  
|<span data-ttu-id="1f6a0-153">Aksi takdirde</span><span class="sxs-lookup"><span data-stu-id="1f6a0-153">otherwise</span></span>|<span data-ttu-id="1f6a0-154">Merhaba hiçbiri kullanılan hello İlkesi parçacığı toobe içeren `when` koşulları değerlendirin çok`true`.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-154">Contains hello policy snippet toobe used if none of hello `when` conditions evaluate too`true`.</span></span>|<span data-ttu-id="1f6a0-155">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-155">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1f6a0-156">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="1f6a0-156">Attributes</span></span>  
  
|<span data-ttu-id="1f6a0-157">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="1f6a0-157">Attribute</span></span>|<span data-ttu-id="1f6a0-158">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-158">Description</span></span>|<span data-ttu-id="1f6a0-159">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-159">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="1f6a0-160">koşul = "Boole ifadesi &#124; Boole sabiti"</span><span class="sxs-lookup"><span data-stu-id="1f6a0-160">condition="Boolean expression &#124; Boolean constant"</span></span>|<span data-ttu-id="1f6a0-161">Merhaba Boole ifadesi veya ne zaman içeren hello sabit tooevaluated `when` ilke bildirimi değerlendirildiği.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-161">hello Boolean expression or constant tooevaluated when hello containing `when` policy statement is evaluated.</span></span>|<span data-ttu-id="1f6a0-162">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-162">Yes</span></span>|  
  
###  <span data-ttu-id="1f6a0-163"><a name="ChooseUsage"></a>Kullanım</span><span class="sxs-lookup"><span data-stu-id="1f6a0-163"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="1f6a0-164">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1f6a0-164">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1f6a0-165">**İlke bölümleri:** gelen, giden arka uç, hata</span><span class="sxs-lookup"><span data-stu-id="1f6a0-165">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1f6a0-166">**İlke kapsamları:** tüm kapsamlar</span><span class="sxs-lookup"><span data-stu-id="1f6a0-166">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="1f6a0-167"><a name="ForwardRequest"></a>İstek</span><span class="sxs-lookup"><span data-stu-id="1f6a0-167"><a name="ForwardRequest"></a> Forward request</span></span>  
 <span data-ttu-id="1f6a0-168">Merhaba `forward-request` İlkesi iletir hello gelen isteği toohello arka uç hizmeti hello istekte belirtilen [bağlamı](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="1f6a0-168">hello `forward-request` policy forwards hello incoming request toohello backend service specified in hello request [context](api-management-policy-expressions.md#ContextVariables).</span></span> <span data-ttu-id="1f6a0-169">Merhaba arka uç hizmeti URL'si hello API belirtilen [ayarları](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) ve hello kullanılarak değiştirilebilir [ayarlamak arka uç hizmetini](api-management-transformation-policies.md) ilkesi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-169">hello backend service URL is specified in hello API  [settings](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) and can be changed using hello [set backend service](api-management-transformation-policies.md) policy.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="1f6a0-170">Bu ilke sonuçlarını hello giden bölümünde toohello arka uç hizmeti ve hello ilkeleri iletilen değil hello isteğindeki değerlendirilir hemen hello başarılı hello hello ilkelerinde tamamlanmasından sonra kaldırma gelen bölümü.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-170">Removing this policy results in hello request not being forwarded toohello backend service and hello policies in hello outbound section are evaluated immediately upon hello successful completion of hello policies in hello inbound section.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1f6a0-171">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-171">Policy statement</span></span>  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a><span data-ttu-id="1f6a0-172">Örnekler</span><span class="sxs-lookup"><span data-stu-id="1f6a0-172">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="1f6a0-173">Örnek</span><span class="sxs-lookup"><span data-stu-id="1f6a0-173">Example</span></span>  
 <span data-ttu-id="1f6a0-174">Merhaba aşağıdaki API düzeyi ilkesi tüm istekleri toohello arka uç hizmeti 60 saniye cinsinden bir zaman aşımı aralığı ile iletir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-174">hello following API level policy forwards all requests toohello backend service with a timeout interval of 60 seconds.</span></span>  
  
```xml  
<!-- api level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="60"/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="1f6a0-175">Örnek</span><span class="sxs-lookup"><span data-stu-id="1f6a0-175">Example</span></span>  
 <span data-ttu-id="1f6a0-176">Bu işlem düzeyi ilkeyi hello kullanan `base` öğesi tooinherit hello arka uç hello üst API düzeyi kapsam ilkesinden.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-176">This operation level policy uses hello `base` element tooinherit hello backend policy from hello parent API level scope.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <base/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="1f6a0-177">Örnek</span><span class="sxs-lookup"><span data-stu-id="1f6a0-177">Example</span></span>  
 <span data-ttu-id="1f6a0-178">Bu işlem düzeyi ilkesi açıkça tüm istekleri toohello arka uç hizmeti ile bir zaman aşımı süresi 120 iletir ve hello üst API düzeyi arka uç İlkesi devralmaz.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-178">This operation level policy explicitly forwards all requests toohello backend service with a timeout of 120 and does not inherit hello parent API level backend policy.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="120"/>   
        <!-- effective policy. note hello absence of <base/> -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="1f6a0-179">Örnek</span><span class="sxs-lookup"><span data-stu-id="1f6a0-179">Example</span></span>  
 <span data-ttu-id="1f6a0-180">Bu işlem düzeyi ilkesi isteklerini iletmek değil toohello arka uç hizmeti.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-180">This operation level policy does not forward requests toohello backend service.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <!-- no forwarding toobackend -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="1f6a0-181">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="1f6a0-181">Elements</span></span>  
  
|<span data-ttu-id="1f6a0-182">Öğesi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-182">Element</span></span>|<span data-ttu-id="1f6a0-183">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-183">Description</span></span>|<span data-ttu-id="1f6a0-184">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-184">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1f6a0-185">İletme isteği</span><span class="sxs-lookup"><span data-stu-id="1f6a0-185">forward-request</span></span>|<span data-ttu-id="1f6a0-186">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-186">Root element.</span></span>|<span data-ttu-id="1f6a0-187">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-187">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1f6a0-188">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="1f6a0-188">Attributes</span></span>  
  
|<span data-ttu-id="1f6a0-189">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="1f6a0-189">Attribute</span></span>|<span data-ttu-id="1f6a0-190">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-190">Description</span></span>|<span data-ttu-id="1f6a0-191">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-191">Required</span></span>|<span data-ttu-id="1f6a0-192">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="1f6a0-192">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="1f6a0-193">zaman aşımı = "tamsayı"</span><span class="sxs-lookup"><span data-stu-id="1f6a0-193">timeout="integer"</span></span>|<span data-ttu-id="1f6a0-194">Merhaba çağrısı toohello arka uç hizmeti önceki saniye cinsinden zaman aşımı aralığı Hello başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-194">hello timeout interval in seconds before hello call toohello backend service fails.</span></span>|<span data-ttu-id="1f6a0-195">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-195">No</span></span>|<span data-ttu-id="1f6a0-196">Hiçbir zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="1f6a0-196">No timeout</span></span>|  
|<span data-ttu-id="1f6a0-197">yeniden yönlendirmeleri izleyin = "true &#124; false"</span><span class="sxs-lookup"><span data-stu-id="1f6a0-197">follow-redirects="true &#124; false"</span></span>|<span data-ttu-id="1f6a0-198">Yeniden yönlendirmeleri hello arka uç hizmetinden hello gateway tarafından izlenen veya toohello çağıran döndürülen olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-198">Specifies whether redirects from hello backend service are followed by hello gateway or returned toohello caller.</span></span>|<span data-ttu-id="1f6a0-199">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-199">No</span></span>|<span data-ttu-id="1f6a0-200">False</span><span class="sxs-lookup"><span data-stu-id="1f6a0-200">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1f6a0-201">Kullanım</span><span class="sxs-lookup"><span data-stu-id="1f6a0-201">Usage</span></span>  
 <span data-ttu-id="1f6a0-202">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1f6a0-202">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1f6a0-203">**İlke bölümleri:** arka uç</span><span class="sxs-lookup"><span data-stu-id="1f6a0-203">**Policy sections:** backend</span></span>  
  
-   <span data-ttu-id="1f6a0-204">**İlke kapsamları:** tüm kapsamlar</span><span class="sxs-lookup"><span data-stu-id="1f6a0-204">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="1f6a0-205"><a name="LimitConcurrency"></a>Sınır eşzamanlılık</span><span class="sxs-lookup"><span data-stu-id="1f6a0-205"><a name="LimitConcurrency"></a> Limit concurrency</span></span>  
 <span data-ttu-id="1f6a0-206">Merhaba `limit-concurrency` ilke tarafından belirtilen istek sayısının belirli bir zamanda hello fazlasını yürütülmesini kapalı ilkeleri engeller.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-206">hello `limit-concurrency` policy prevents enclosed policies from executing by more than hello specified number of requests at a given time.</span></span> <span data-ttu-id="1f6a0-207">Merhaba Eşiği aşan bağlı Hello en büyük sıra uzunluğu elde kadar yeni istekler tooa sıra eklenir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-207">Upon exceeding hello threshold, new requests are added tooa queue, until hello maximum queue length is achieved.</span></span> <span data-ttu-id="1f6a0-208">Sıra Tükenme yeni istekleri hemen başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-208">Upon queue exhaustion, new requests will fail immediately.</span></span>
  
###  <span data-ttu-id="1f6a0-209"><a name="LimitConcurrencyStatement"></a>İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-209"><a name="LimitConcurrencyStatement"></a> Policy statement</span></span>  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a><span data-ttu-id="1f6a0-210">Örnekler</span><span class="sxs-lookup"><span data-stu-id="1f6a0-210">Examples</span></span>  
  
####  <span data-ttu-id="1f6a0-211"><a name="ChooseExample"></a>Örnek</span><span class="sxs-lookup"><span data-stu-id="1f6a0-211"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="1f6a0-212">Merhaba aşağıdaki örnekte nasıl toolimit istek sayısı bir bağlamının hello değere göre tooa arka uç iletilen gösterir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-212">hello following example demonstrates how toolimit number of requests forwarded tooa backend based on hello value of a context variable.</span></span>
 
```xml  
<policies>
  <inbound>…</inbound>
  <backend>
    <limit-concurrency key="@((string)context.Variables["connectionId"])" max-count="3" timeout="60">
      <forward-request timeout="120"/>
    <limit-concurrency/>
  </backend>
  <outbound>…</outbound>
</policies>
```

### <a name="elements"></a><span data-ttu-id="1f6a0-213">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="1f6a0-213">Elements</span></span>  
  
|<span data-ttu-id="1f6a0-214">Öğesi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-214">Element</span></span>|<span data-ttu-id="1f6a0-215">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-215">Description</span></span>|<span data-ttu-id="1f6a0-216">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-216">Required</span></span>|  
|-------------|-----------------|--------------|    
|<span data-ttu-id="1f6a0-217">sınır eşzamanlılık</span><span class="sxs-lookup"><span data-stu-id="1f6a0-217">limit-concurrency</span></span>|<span data-ttu-id="1f6a0-218">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-218">Root element.</span></span>|<span data-ttu-id="1f6a0-219">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1f6a0-220">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="1f6a0-220">Attributes</span></span>  
  
|<span data-ttu-id="1f6a0-221">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="1f6a0-221">Attribute</span></span>|<span data-ttu-id="1f6a0-222">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-222">Description</span></span>|<span data-ttu-id="1f6a0-223">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-223">Required</span></span>|<span data-ttu-id="1f6a0-224">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="1f6a0-224">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="1f6a0-225">anahtar</span><span class="sxs-lookup"><span data-stu-id="1f6a0-225">key</span></span>|<span data-ttu-id="1f6a0-226">Bir dize.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-226">A string.</span></span> <span data-ttu-id="1f6a0-227">İzin verilen ifade.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-227">Expression allowed.</span></span> <span data-ttu-id="1f6a0-228">Merhaba eşzamanlılık kapsamını belirtir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-228">Specifies hello concurrency scope.</span></span> <span data-ttu-id="1f6a0-229">Birden çok ilke tarafından paylaşılabilir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-229">Can be shared by multiple policies.</span></span>|<span data-ttu-id="1f6a0-230">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-230">Yes</span></span>|<span data-ttu-id="1f6a0-231">Yok</span><span class="sxs-lookup"><span data-stu-id="1f6a0-231">N/A</span></span>|  
|<span data-ttu-id="1f6a0-232">en yüksek sayısı</span><span class="sxs-lookup"><span data-stu-id="1f6a0-232">max-count</span></span>|<span data-ttu-id="1f6a0-233">Bir tam sayı.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-233">An integer.</span></span> <span data-ttu-id="1f6a0-234">En fazla bir tooenter hello ilkesi izin verilen istek sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-234">Specifies a maximum number of requests that are allowed tooenter hello policy.</span></span>|<span data-ttu-id="1f6a0-235">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-235">Yes</span></span>|<span data-ttu-id="1f6a0-236">Yok</span><span class="sxs-lookup"><span data-stu-id="1f6a0-236">N/A</span></span>|  
|<span data-ttu-id="1f6a0-237">Zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="1f6a0-237">timeout</span></span>|<span data-ttu-id="1f6a0-238">Bir tam sayı.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-238">An integer.</span></span> <span data-ttu-id="1f6a0-239">İzin verilen ifade.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-239">Expression allowed.</span></span> <span data-ttu-id="1f6a0-240">Merhaba bir istek tooenter bir kapsam ile başarısız olmadan önce beklemesi gereken saniye sayısını belirtir "403 çok sayıda istek"</span><span class="sxs-lookup"><span data-stu-id="1f6a0-240">Specifies hello number of seconds a request should wait tooenter a scope before failing with "403 Too Many Requests"</span></span>|<span data-ttu-id="1f6a0-241">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-241">No</span></span>|<span data-ttu-id="1f6a0-242">Infinity</span><span class="sxs-lookup"><span data-stu-id="1f6a0-242">Infinity</span></span>|  
|<span data-ttu-id="1f6a0-243">en büyük sıra uzunluğu</span><span class="sxs-lookup"><span data-stu-id="1f6a0-243">max-queue-length</span></span>|<span data-ttu-id="1f6a0-244">Bir tam sayı.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-244">An integer.</span></span> <span data-ttu-id="1f6a0-245">İzin verilen ifade.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-245">Expression allowed.</span></span> <span data-ttu-id="1f6a0-246">Merhaba en büyük sıra uzunluğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-246">Specifies hello maximum queue length.</span></span> <span data-ttu-id="1f6a0-247">Gelen istekleri tooenter çalışırken bu ilke ile sona erdirilecek "403 çok sayıda istek" hemen zaman hello sırası tükendi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-247">Incoming requests trying tooenter this policy will be terminated with “403 Too Many Requests” immediately when hello queue is exhausted.</span></span>|<span data-ttu-id="1f6a0-248">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-248">No</span></span>|<span data-ttu-id="1f6a0-249">Infinity</span><span class="sxs-lookup"><span data-stu-id="1f6a0-249">Infinity</span></span>|  
  
###  <span data-ttu-id="1f6a0-250"><a name="ChooseUsage"></a>Kullanım</span><span class="sxs-lookup"><span data-stu-id="1f6a0-250"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="1f6a0-251">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1f6a0-251">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1f6a0-252">**İlke bölümleri:** gelen, giden arka uç, hata</span><span class="sxs-lookup"><span data-stu-id="1f6a0-252">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1f6a0-253">**İlke kapsamları:** tüm kapsamlar</span><span class="sxs-lookup"><span data-stu-id="1f6a0-253">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="1f6a0-254"><a name="log-to-eventhub"></a>Günlük tooEvent Hub</span><span class="sxs-lookup"><span data-stu-id="1f6a0-254"><a name="log-to-eventhub"></a> Log tooEvent Hub</span></span>  
 <span data-ttu-id="1f6a0-255">Merhaba `log-to-eventhub` hello iletilerinde belirtilen biçim tooan Event Hub'ın Günlükçü varlık tarafından tanımlanan ilke gönderir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-255">hello `log-to-eventhub` policy sends messages in hello specified format tooan Event Hub defined by a Logger entity.</span></span> <span data-ttu-id="1f6a0-256">Adından da anlaşılacağı gibi hello İlkesi çevrimiçi veya çevrimdışı analiz için seçilen istek veya yanıt bağlam bilgilerini kaydetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-256">As its name implies, hello policy is used for saving selected request or response context information for online or offline analysis.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="1f6a0-257">Bir olay hub'ı ve olayları günlüğe kaydetmeyi yapılandırma hakkında adım adım yönergeler için bkz: [nasıl toolog API Management olayları Azure Event Hubs ile](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="1f6a0-257">For a step-by-step guide on configuring an event hub and logging events, see [How toolog API Management events with Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1f6a0-258">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-258">Policy statement</span></span>  
  
```xml  
<log-to-eventhub logger-id="id of hello logger entity" partition-id="index of hello partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string toobe logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a><span data-ttu-id="1f6a0-259">Örnek</span><span class="sxs-lookup"><span data-stu-id="1f6a0-259">Example</span></span>  
 <span data-ttu-id="1f6a0-260">Herhangi bir dize, olay hub ' oturum hello değeri toobe olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-260">Any string can be used as hello value toobe logged in Event Hubs.</span></span> <span data-ttu-id="1f6a0-261">Bu örnekte hello tarih ve saat dağıtım hizmet adı, istek kimliği, IP adresi ve tüm gelen çağrıları için işlem adı oturum toohello event hub'ı Günlükçü hello ile kayıtlı olan `contoso-logger` kimliği.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-261">In this example hello date and time, deployment service name, request id, ip address, and operation name for all inbound calls are logged toohello event hub Logger registered with hello `contoso-logger` id.</span></span>  
  
```xml  
<policies>  
  <inbound>  
    <log-to-eventhub logger-id ='contoso-logger'>  
      @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name) )   
    </log-to-eventhub>  
  </inbound>  
  <outbound>          
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="1f6a0-262">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="1f6a0-262">Elements</span></span>  
  
|<span data-ttu-id="1f6a0-263">Öğesi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-263">Element</span></span>|<span data-ttu-id="1f6a0-264">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-264">Description</span></span>|<span data-ttu-id="1f6a0-265">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-265">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1f6a0-266">Günlük eventhub</span><span class="sxs-lookup"><span data-stu-id="1f6a0-266">log-to-eventhub</span></span>|<span data-ttu-id="1f6a0-267">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-267">Root element.</span></span> <span data-ttu-id="1f6a0-268">Merhaba bu öğenin hello dize toolog tooyour olay hub'ı değerdir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-268">hello value of this element is hello string toolog tooyour event hub.</span></span>|<span data-ttu-id="1f6a0-269">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-269">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1f6a0-270">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="1f6a0-270">Attributes</span></span>  
  
|<span data-ttu-id="1f6a0-271">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="1f6a0-271">Attribute</span></span>|<span data-ttu-id="1f6a0-272">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-272">Description</span></span>|<span data-ttu-id="1f6a0-273">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-273">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="1f6a0-274">Günlükçü kimliği</span><span class="sxs-lookup"><span data-stu-id="1f6a0-274">logger-id</span></span>|<span data-ttu-id="1f6a0-275">Merhaba Hello kimliğini Günlükçü API Management hizmetiniz ile kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-275">hello id of hello Logger registered with your API Management service.</span></span>|<span data-ttu-id="1f6a0-276">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-276">Yes</span></span>|  
|<span data-ttu-id="1f6a0-277">bölüm kimliği</span><span class="sxs-lookup"><span data-stu-id="1f6a0-277">partition-id</span></span>|<span data-ttu-id="1f6a0-278">İletilerin gönderileceği hello bölümünün başlangıç dizinini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-278">Specifies hello index of hello partition where messages are sent.</span></span>|<span data-ttu-id="1f6a0-279">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-279">Optional.</span></span> <span data-ttu-id="1f6a0-280">Bu öznitelik, kullanılamaz. `partition-key` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-280">This attribute may not be used if `partition-key` is used.</span></span>|  
|<span data-ttu-id="1f6a0-281">Bölüm anahtarı</span><span class="sxs-lookup"><span data-stu-id="1f6a0-281">partition-key</span></span>|<span data-ttu-id="1f6a0-282">İleti gönderildiğinde bölüm ataması için kullanılan başlangıç değerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-282">Specifies hello value used for partition assignment when messages are sent.</span></span>|<span data-ttu-id="1f6a0-283">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-283">Optional.</span></span> <span data-ttu-id="1f6a0-284">Bu öznitelik, kullanılamaz. `partition-id` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-284">This attribute may not be used if `partition-id` is used.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1f6a0-285">Kullanım</span><span class="sxs-lookup"><span data-stu-id="1f6a0-285">Usage</span></span>  
 <span data-ttu-id="1f6a0-286">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1f6a0-286">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1f6a0-287">**İlke bölümleri:** gelen, giden arka uç, hata</span><span class="sxs-lookup"><span data-stu-id="1f6a0-287">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1f6a0-288">**İlke kapsamları:** tüm kapsamlar</span><span class="sxs-lookup"><span data-stu-id="1f6a0-288">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="1f6a0-289"><a name="mock-response"></a>Sahte yanıt</span><span class="sxs-lookup"><span data-stu-id="1f6a0-289"><a name="mock-response"></a> Mock response</span></span>  
<span data-ttu-id="1f6a0-290">Merhaba `mock-response`, hello adından da anlaşılacağı, olan kullanılan toomock API'ler ve işlemler.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-290">hello `mock-response`, as hello name implies, is used toomock APIs and operations.</span></span> <span data-ttu-id="1f6a0-291">Normal ardışık düzen yürütmesi durdurur ve mocked yanıt toohello çağıran döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-291">It aborts normal pipeline execution and returns a mocked response toohello caller.</span></span> <span data-ttu-id="1f6a0-292">Hello İlkesi her zaman en yüksek doğruluk tooreturn yanıtların çalışır.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-292">hello policy always tries tooreturn responses of highest fidelity.</span></span> <span data-ttu-id="1f6a0-293">Bu yanıt içerik örnekler, kullanılabilir olduğunda tercih eder.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-293">It prefers response content examples, whenever available.</span></span> <span data-ttu-id="1f6a0-294">Bu örnek yanıtları şemalarına dönüştürmeyi, şemaları sağlanır ve örnekler olmadıkları zaman oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-294">It generates sample responses from schemas, when schemas are provided and examples are not.</span></span> <span data-ttu-id="1f6a0-295">Örnek ya da şemaları bulunursa, içerik ile yanıtları döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-295">If neither examples or schemas are found, responses with no content are returned.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="1f6a0-296">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-296">Policy statement</span></span>  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="1f6a0-297">Örnekler</span><span class="sxs-lookup"><span data-stu-id="1f6a0-297">Examples</span></span>  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, hello content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, hello content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a><span data-ttu-id="1f6a0-298">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="1f6a0-298">Elements</span></span>  
  
|<span data-ttu-id="1f6a0-299">Öğesi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-299">Element</span></span>|<span data-ttu-id="1f6a0-300">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-300">Description</span></span>|<span data-ttu-id="1f6a0-301">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-301">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1f6a0-302">mock yanıt</span><span class="sxs-lookup"><span data-stu-id="1f6a0-302">mock-response</span></span>|<span data-ttu-id="1f6a0-303">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-303">Root element.</span></span>|<span data-ttu-id="1f6a0-304">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-304">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1f6a0-305">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="1f6a0-305">Attributes</span></span>  
  
|<span data-ttu-id="1f6a0-306">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="1f6a0-306">Attribute</span></span>|<span data-ttu-id="1f6a0-307">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-307">Description</span></span>|<span data-ttu-id="1f6a0-308">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-308">Required</span></span>|<span data-ttu-id="1f6a0-309">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="1f6a0-309">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="1f6a0-310">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="1f6a0-310">status-code</span></span>|<span data-ttu-id="1f6a0-311">Yanıt durum kodu belirtir ve kullanılan tooselect karşılık gelen örnek veya şema.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-311">Specifies response status code and is used tooselect corresponding example or schema.</span></span>|<span data-ttu-id="1f6a0-312">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-312">No</span></span>|<span data-ttu-id="1f6a0-313">200</span><span class="sxs-lookup"><span data-stu-id="1f6a0-313">200</span></span>|  
|<span data-ttu-id="1f6a0-314">içerik türü</span><span class="sxs-lookup"><span data-stu-id="1f6a0-314">content-type</span></span>|<span data-ttu-id="1f6a0-315">Belirtir `Content-Type` yanıt üstbilgi değeri ve kullanılan tooselect karşılık gelen örnek veya şema.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-315">Specifies `Content-Type` response header value and is used tooselect corresponding example or schema.</span></span>|<span data-ttu-id="1f6a0-316">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-316">No</span></span>|<span data-ttu-id="1f6a0-317">None</span><span class="sxs-lookup"><span data-stu-id="1f6a0-317">None</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1f6a0-318">Kullanım</span><span class="sxs-lookup"><span data-stu-id="1f6a0-318">Usage</span></span>  
 <span data-ttu-id="1f6a0-319">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1f6a0-319">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1f6a0-320">**İlke bölümleri:** gelen, giden, hata</span><span class="sxs-lookup"><span data-stu-id="1f6a0-320">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="1f6a0-321">**İlke kapsamları:** tüm kapsamlar</span><span class="sxs-lookup"><span data-stu-id="1f6a0-321">**Policy scopes:** all scopes</span></span>

##  <span data-ttu-id="1f6a0-322"><a name="Retry"></a>Yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="1f6a0-322"><a name="Retry"></a> Retry</span></span>  
 <span data-ttu-id="1f6a0-323">Hello `retry` İlkesi kendi alt ilkeleri bir kez çalıştırır ve bunların yürütme hello yeniden deneme kadar yeniden deneme `condition` olur `false` ya da yeniden deneme `count` tükendi olduğu.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-323">hello             `retry` policy executes its child policies once and then retries their execution until hello retry `condition` becomes            `false` or retry            `count` is exhausted.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1f6a0-324">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-324">Policy statement</span></span>  
  
```xml  
  
<retry  
    condition="boolean expression or literal"  
    count="number of retry attempts"  
    interval="retry interval in seconds"  
    max-interval="maximum retry interval in seconds"  
    delta="retry interval delta in seconds"  
    first-fast-retry="boolean expression or literal">  
        <!-- One or more child policies. No restrictions -->  
</retry>  
  
```  
  
### <a name="example"></a><span data-ttu-id="1f6a0-325">Örnek</span><span class="sxs-lookup"><span data-stu-id="1f6a0-325">Example</span></span>  
 <span data-ttu-id="1f6a0-326">Hello örnek istek forewarding aşağıdaki üstel yeniden deneme algoritması kullanılarak kez tooten yukarı yapılmaya çalışıldı.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-326">In hello following example request forewarding is retried up tooten times using exponential retry algorithm.</span></span> <span data-ttu-id="1f6a0-327">Bu yana `first-fast-retry` toofalse, ayarlanan tüm denemeleri konu toohello exponsntial yeniden deneme algoritması olan.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-327">Since                    `first-fast-retry` is set toofalse, all retry attempts are subject toohello exponsntial retry algorithm.</span></span>  
  
```xml  
  
<retry  
    condition="@(context.Response.StatusCode == 500)"  
    count="10"  
    interval="10"  
    max-interval="100"  
    delta="10"  
    first-fast-retry="false">  
        <forward-request />  
</retry>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="1f6a0-328">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="1f6a0-328">Elements</span></span>  
  
|<span data-ttu-id="1f6a0-329">Öğesi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-329">Element</span></span>|<span data-ttu-id="1f6a0-330">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-330">Description</span></span>|<span data-ttu-id="1f6a0-331">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-331">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1f6a0-332">Yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="1f6a0-332">retry</span></span>|<span data-ttu-id="1f6a0-333">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-333">Root element.</span></span> <span data-ttu-id="1f6a0-334">Diğer ilkeleri ve alt öğeleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-334">May contain any other policies as its child elements.</span></span>|<span data-ttu-id="1f6a0-335">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-335">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1f6a0-336">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="1f6a0-336">Attributes</span></span>  
  
|<span data-ttu-id="1f6a0-337">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="1f6a0-337">Attribute</span></span>|<span data-ttu-id="1f6a0-338">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-338">Description</span></span>|<span data-ttu-id="1f6a0-339">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-339">Required</span></span>|<span data-ttu-id="1f6a0-340">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="1f6a0-340">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="1f6a0-341">Koşul</span><span class="sxs-lookup"><span data-stu-id="1f6a0-341">condition</span></span>|<span data-ttu-id="1f6a0-342">Boole bir hazır değer veya [ifade](api-management-policy-expressions.md) yeniden deneme durmuş olup belirtme (`false`) veya devam (`true`).</span><span class="sxs-lookup"><span data-stu-id="1f6a0-342">A boolean literal or [expression](api-management-policy-expressions.md) specifying if retries should be stopped (`false`) or continued (`true`).</span></span>|<span data-ttu-id="1f6a0-343">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-343">Yes</span></span>|<span data-ttu-id="1f6a0-344">Yok</span><span class="sxs-lookup"><span data-stu-id="1f6a0-344">N/A</span></span>|  
|<span data-ttu-id="1f6a0-345">Sayısı</span><span class="sxs-lookup"><span data-stu-id="1f6a0-345">count</span></span>|<span data-ttu-id="1f6a0-346">En fazla yeniden deneme tooattempt Hello yineleneceğini belirten pozitif bir sayı.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-346">A positive number specifying hello maximum number of retries tooattempt.</span></span>|<span data-ttu-id="1f6a0-347">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-347">Yes</span></span>|<span data-ttu-id="1f6a0-348">Yok</span><span class="sxs-lookup"><span data-stu-id="1f6a0-348">N/A</span></span>|  
|<span data-ttu-id="1f6a0-349">interval</span><span class="sxs-lookup"><span data-stu-id="1f6a0-349">interval</span></span>|<span data-ttu-id="1f6a0-350">Merhaba bekleme hello yeniden deneme aralığını belirterek saniye cinsinden pozitif bir sayı.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-350">A positive number in seconds specifying hello wait interval between hello retry attempts.</span></span>|<span data-ttu-id="1f6a0-351">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-351">Yes</span></span>|<span data-ttu-id="1f6a0-352">Yok</span><span class="sxs-lookup"><span data-stu-id="1f6a0-352">N/A</span></span>|  
|<span data-ttu-id="1f6a0-353">en fazla aralığı</span><span class="sxs-lookup"><span data-stu-id="1f6a0-353">max-interval</span></span>|<span data-ttu-id="1f6a0-354">Merhaba en fazla bekleme hello yeniden deneme aralığını belirterek saniye cinsinden pozitif bir sayı.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-354">A positive number in seconds specifying hello maximum wait interval between hello retry attempts.</span></span> <span data-ttu-id="1f6a0-355">Kullanılan tooimplement üstel yeniden deneme algoritması olur.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-355">It is used tooimplement an exponential retry algorithm.</span></span>|<span data-ttu-id="1f6a0-356">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-356">No</span></span>|<span data-ttu-id="1f6a0-357">Yok</span><span class="sxs-lookup"><span data-stu-id="1f6a0-357">N/A</span></span>|  
|<span data-ttu-id="1f6a0-358">Delta</span><span class="sxs-lookup"><span data-stu-id="1f6a0-358">delta</span></span>|<span data-ttu-id="1f6a0-359">Merhaba bekleme aralığı artırma belirtme saniye cinsinden pozitif bir sayı.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-359">A positive number in seconds specifying hello wait interval increment.</span></span> <span data-ttu-id="1f6a0-360">Kullanılan tooimplement hello doğrusal ve üstel yeniden deneme algoritmaları olur.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-360">It is used tooimplement hello linear and exponential retry algorithms.</span></span>|<span data-ttu-id="1f6a0-361">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-361">No</span></span>|<span data-ttu-id="1f6a0-362">Yok</span><span class="sxs-lookup"><span data-stu-id="1f6a0-362">N/A</span></span>|  
|<span data-ttu-id="1f6a0-363">ilk hızlı yeniden</span><span class="sxs-lookup"><span data-stu-id="1f6a0-363">first-fast-retry</span></span>|<span data-ttu-id="1f6a0-364">Varsa çok ayarlamak `true` , hello ilk yeniden deneme girişimi hemen gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-364">If set too                                   `true` , hello first retry attempt is performed immediately.</span></span>|<span data-ttu-id="1f6a0-365">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-365">No</span></span>|`false`|  
  
> [!NOTE]
>  <span data-ttu-id="1f6a0-366">Ne zaman yalnızca hello `interval` belirtilirse, **sabit** aralığı yeniden denemeler gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-366">When only hello `interval` is specified, **fixed** interval retries are performed.</span></span>  
>  <span data-ttu-id="1f6a0-367">Ne zaman yalnızca hello `interval` ve `delta` belirtilir, bir **doğrusal** aralığı yeniden deneme algoritması kullanılır, denemeler arasındaki bekleme süresini hesaplanan according hello olduğu formülü - aşağıdaki `interval + (count - 1)*delta`.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-367">When only hello `interval` and `delta` are specified, a **linear** interval retry algorithm is used, where wait time between retries is calculated according hello following formula - `interval + (count - 1)*delta`.</span></span>  
>  <span data-ttu-id="1f6a0-368">Ne zaman hello `interval`, `max-interval` ve `delta` belirtilir, **üstel** aralığı yeniden deneme algoritması uygulandığında, burada hello bekleme süresi hello denemeler arasındaki Başlangıçdeğerindenkatlanarakartıyor`interval`toohello değeri `max-interval` toohello aşağıdaki göre forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-368">When hello `interval`, `max-interval` and `delta` are specified, **exponential** interval retry algorithm is applied, where hello wait time between hello retries is growing exponentially from hello value of `interval` toohello value `max-interval` according toohello following forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span></span>  
  
### <a name="usage"></a><span data-ttu-id="1f6a0-369">Kullanım</span><span class="sxs-lookup"><span data-stu-id="1f6a0-369">Usage</span></span>  
 <span data-ttu-id="1f6a0-370">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="1f6a0-370">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span> <span data-ttu-id="1f6a0-371">Alt İlkesi kullanım kısıtlamaları Bu ilke tarafından devralınır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-371">Note that child policy usage restrictions will be inherited by this policy.</span></span>  
  
-   <span data-ttu-id="1f6a0-372">**İlke bölümleri:** gelen, giden arka uç, hata</span><span class="sxs-lookup"><span data-stu-id="1f6a0-372">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1f6a0-373">**İlke kapsamları:** tüm kapsamlar</span><span class="sxs-lookup"><span data-stu-id="1f6a0-373">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="1f6a0-374"><a name="ReturnResponse"></a>Yanıt döndürür</span><span class="sxs-lookup"><span data-stu-id="1f6a0-374"><a name="ReturnResponse"></a> Return response</span></span>  
 <span data-ttu-id="1f6a0-375">Merhaba `return-response` İlkesi ardışık düzen yürütmesi durdurur ve bir varsayılan veya özel yanıt toohello çağıran döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-375">hello `return-response` policy aborts pipeline execution and returns either a default or custom response toohello caller.</span></span> <span data-ttu-id="1f6a0-376">Varsayılan yanıt `200 OK` hiçbir gövde ile.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-376">Default response is `200 OK` with no body.</span></span> <span data-ttu-id="1f6a0-377">Özel yanıtı bağlam değişkeni veya ilke deyimleri ile belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-377">Custom response can be specified via a context variable or policy statements.</span></span> <span data-ttu-id="1f6a0-378">Her ikisi de sağlandığında, hello bağlamının içinde yer alan hello yanıt toohello çağıran döndürülen önce hello İlkesi deyimleri tarafından değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-378">When both are provided, hello response contained within hello context variable is modified by hello policy statements before being returned toohello caller.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1f6a0-379">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-379">Policy statement</span></span>  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a><span data-ttu-id="1f6a0-380">Örnek</span><span class="sxs-lookup"><span data-stu-id="1f6a0-380">Example</span></span>  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="1f6a0-381">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="1f6a0-381">Elements</span></span>  
  
|<span data-ttu-id="1f6a0-382">Öğesi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-382">Element</span></span>|<span data-ttu-id="1f6a0-383">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-383">Description</span></span>|<span data-ttu-id="1f6a0-384">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-384">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1f6a0-385">return yanıt</span><span class="sxs-lookup"><span data-stu-id="1f6a0-385">return-response</span></span>|<span data-ttu-id="1f6a0-386">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-386">Root element.</span></span>|<span data-ttu-id="1f6a0-387">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-387">Yes</span></span>|  
|<span data-ttu-id="1f6a0-388">set üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-388">set-header</span></span>|<span data-ttu-id="1f6a0-389">A [set üstbilgisi](api-management-transformation-policies.md#SetHTTPheader) ilke bildirimi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-389">A [set-header](api-management-transformation-policies.md#SetHTTPheader) policy statement.</span></span>|<span data-ttu-id="1f6a0-390">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-390">No</span></span>|  
|<span data-ttu-id="1f6a0-391">set-gövdesi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-391">set-body</span></span>|<span data-ttu-id="1f6a0-392">A [kümesi gövde](api-management-transformation-policies.md#SetBody) ilke bildirimi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-392">A [set-body](api-management-transformation-policies.md#SetBody) policy statement.</span></span>|<span data-ttu-id="1f6a0-393">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-393">No</span></span>|  
|<span data-ttu-id="1f6a0-394">durumunu ayarla</span><span class="sxs-lookup"><span data-stu-id="1f6a0-394">set-status</span></span>|<span data-ttu-id="1f6a0-395">A [durumunu ayarla](api-management-advanced-policies.md#SetStatus) ilke bildirimi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-395">A [set-status](api-management-advanced-policies.md#SetStatus) policy statement.</span></span>|<span data-ttu-id="1f6a0-396">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-396">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1f6a0-397">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="1f6a0-397">Attributes</span></span>  
  
|<span data-ttu-id="1f6a0-398">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="1f6a0-398">Attribute</span></span>|<span data-ttu-id="1f6a0-399">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-399">Description</span></span>|<span data-ttu-id="1f6a0-400">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-400">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="1f6a0-401">yanıt değişken adı</span><span class="sxs-lookup"><span data-stu-id="1f6a0-401">response-variable-name</span></span>|<span data-ttu-id="1f6a0-402">Merhaba hello bağlamının adı, örneğin, Yukarı Akış başvurulan [gönderme isteği](api-management-advanced-policies.md#SendRequest) ilke ve içeren bir `Response` nesnesi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-402">hello name of hello context variable referenced from, for example, an upstream [send-request](api-management-advanced-policies.md#SendRequest) policy and containing a `Response` object</span></span>|<span data-ttu-id="1f6a0-403">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-403">Optional.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1f6a0-404">Kullanım</span><span class="sxs-lookup"><span data-stu-id="1f6a0-404">Usage</span></span>  
 <span data-ttu-id="1f6a0-405">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1f6a0-405">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1f6a0-406">**İlke bölümleri:** gelen, giden arka uç, hata</span><span class="sxs-lookup"><span data-stu-id="1f6a0-406">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1f6a0-407">**İlke kapsamları:** tüm kapsamlar</span><span class="sxs-lookup"><span data-stu-id="1f6a0-407">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="1f6a0-408"><a name="SendOneWayRequest"></a>Tek yönlü İsteği Gönder</span><span class="sxs-lookup"><span data-stu-id="1f6a0-408"><a name="SendOneWayRequest"></a> Send one way request</span></span>  
 <span data-ttu-id="1f6a0-409">Merhaba `send-one-way-request` ilke toohello belirtilen URL için bir yanıt beklemeden sağlanan hello isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-409">hello `send-one-way-request` policy sends hello provided request toohello specified URL without waiting for a response.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1f6a0-410">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-410">Policy statement</span></span>  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="1f6a0-411">Örnek</span><span class="sxs-lookup"><span data-stu-id="1f6a0-411">Example</span></span>  
 <span data-ttu-id="1f6a0-412">Bu örnek ilke hello kullanmanın bir örneği gösterir `send-one-way-request` İlkesi toosend bir ileti tooa Slack sohbet hello HTTP yanıt kodunu büyük veya ona eşit too500 ise odası.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-412">This sample policy shows an example of using hello `send-one-way-request` policy toosend a message tooa Slack chat room if hello HTTP response code is greater than or equal too500.</span></span> <span data-ttu-id="1f6a0-413">Bu örnek hakkında daha fazla bilgi için bkz: [dış Hizmetleri'nden hello Azure API Management hizmeti kullanarak](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="1f6a0-413">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<choose>  
    <when condition="@(context.Response.StatusCode >= 500)">  
      <send-one-way-request mode="new">  
        <set-url>https://hooks.slack.com/services/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</set-url>  
        <set-method>POST</set-method>  
        <set-body>@{  
                return new JObject(  
                        new JProperty("username","APIM Alert"),  
                        new JProperty("icon_emoji", ":ghost:"),  
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",  
                                                context.Request.Method,  
                                                context.Request.Url.Path + context.Request.Url.QueryString,  
                                                context.Request.Url.Host,  
                                                context.Response.StatusCode,  
                                                context.Response.StatusReason,  
                                                context.User.Email  
                                                ))  
                        ).ToString();  
            }</set-body>  
      </send-one-way-request>  
    </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="1f6a0-414">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="1f6a0-414">Elements</span></span>  
  
|<span data-ttu-id="1f6a0-415">Öğesi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-415">Element</span></span>|<span data-ttu-id="1f6a0-416">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-416">Description</span></span>|<span data-ttu-id="1f6a0-417">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-417">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1f6a0-418">bir şekilde İsteği Gönder</span><span class="sxs-lookup"><span data-stu-id="1f6a0-418">send-one-way-request</span></span>|<span data-ttu-id="1f6a0-419">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-419">Root element.</span></span>|<span data-ttu-id="1f6a0-420">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-420">Yes</span></span>|  
|<span data-ttu-id="1f6a0-421">URL</span><span class="sxs-lookup"><span data-stu-id="1f6a0-421">url</span></span>|<span data-ttu-id="1f6a0-422">Merhaba isteği Hello URL'si.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-422">hello URL of hello request.</span></span>|<span data-ttu-id="1f6a0-423">Hiçbir IF modu kopyalama; = Aksi takdirde Evet.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-423">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="1f6a0-424">Yöntemi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-424">method</span></span>|<span data-ttu-id="1f6a0-425">Merhaba hello isteği için HTTP yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-425">hello HTTP method for hello request.</span></span>|<span data-ttu-id="1f6a0-426">Hiçbir IF modu kopyalama; = Aksi takdirde Evet.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-426">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="1f6a0-427">üst bilgi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-427">header</span></span>|<span data-ttu-id="1f6a0-428">İstek üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-428">Request header.</span></span> <span data-ttu-id="1f6a0-429">Birden çok üstbilgi öğeleri için birden çok istek üstbilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-429">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="1f6a0-430">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-430">No</span></span>|  
|<span data-ttu-id="1f6a0-431">Gövde</span><span class="sxs-lookup"><span data-stu-id="1f6a0-431">body</span></span>|<span data-ttu-id="1f6a0-432">Merhaba istek gövdesi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-432">hello request body.</span></span>|<span data-ttu-id="1f6a0-433">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-433">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1f6a0-434">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="1f6a0-434">Attributes</span></span>  
  
|<span data-ttu-id="1f6a0-435">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="1f6a0-435">Attribute</span></span>|<span data-ttu-id="1f6a0-436">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-436">Description</span></span>|<span data-ttu-id="1f6a0-437">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-437">Required</span></span>|<span data-ttu-id="1f6a0-438">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="1f6a0-438">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="1f6a0-439">modu = "dize"</span><span class="sxs-lookup"><span data-stu-id="1f6a0-439">mode="string"</span></span>|<span data-ttu-id="1f6a0-440">Yeni bir istek veya bir kopyasını hello geçerli istek olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-440">Determines whether this is a new request or a copy of hello current request.</span></span> <span data-ttu-id="1f6a0-441">Giden modunda modu = kopyalama hello istek gövdesi başlatamadı.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-441">In outbound mode, mode=copy does not initialize hello request body.</span></span>|<span data-ttu-id="1f6a0-442">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-442">No</span></span>|<span data-ttu-id="1f6a0-443">Yeni</span><span class="sxs-lookup"><span data-stu-id="1f6a0-443">New</span></span>|  
|<span data-ttu-id="1f6a0-444">ad</span><span class="sxs-lookup"><span data-stu-id="1f6a0-444">name</span></span>|<span data-ttu-id="1f6a0-445">Merhaba hello üstbilgi toobe kümesinin adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-445">Specifies hello name of hello header toobe set.</span></span>|<span data-ttu-id="1f6a0-446">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-446">Yes</span></span>|<span data-ttu-id="1f6a0-447">Yok</span><span class="sxs-lookup"><span data-stu-id="1f6a0-447">N/A</span></span>|  
|<span data-ttu-id="1f6a0-448">Mevcut eylem</span><span class="sxs-lookup"><span data-stu-id="1f6a0-448">exists-action</span></span>|<span data-ttu-id="1f6a0-449">Merhaba üstbilgi zaten belirtildiğinde hangi eylemini tootake belirtir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-449">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="1f6a0-450">Bu öznitelik değerlerini aşağıdaki hello birine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-450">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="1f6a0-451">-değiştirir hello hello varolan üstbilgisinin değerini geçersiz kıl -.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-451">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="1f6a0-452">-skip - hello varolan üstbilgi değeri değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-452">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="1f6a0-453">-Ekle - hello değeri toohello varolan üstbilgi değeri ekler.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-453">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="1f6a0-454">-delete - hello üstbilgisini hello isteğinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-454">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="1f6a0-455">Ayarlandığında çok`override` birden çok girişi kaydetme; hello ile aynı sonuçları (birden çok kez listelenir) kümesi according tooall girdisi olan hello üstbilgisinde adı yalnızca listelenen değerler hello sonucunda ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-455">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="1f6a0-456">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-456">No</span></span>|<span data-ttu-id="1f6a0-457">geçersiz kılma</span><span class="sxs-lookup"><span data-stu-id="1f6a0-457">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1f6a0-458">Kullanım</span><span class="sxs-lookup"><span data-stu-id="1f6a0-458">Usage</span></span>  
 <span data-ttu-id="1f6a0-459">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1f6a0-459">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1f6a0-460">**İlke bölümleri:** gelen, giden arka uç, hata</span><span class="sxs-lookup"><span data-stu-id="1f6a0-460">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1f6a0-461">**İlke kapsamları:** tüm kapsamlar</span><span class="sxs-lookup"><span data-stu-id="1f6a0-461">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="1f6a0-462"><a name="SendRequest"></a>İsteği Gönder</span><span class="sxs-lookup"><span data-stu-id="1f6a0-462"><a name="SendRequest"></a> Send request</span></span>  
 <span data-ttu-id="1f6a0-463">Merhaba `send-request` ilke toohello belirtilen zaman aşımı değerini hello ayarlamak daha artık bekleyen URL, sağlanan hello isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-463">hello `send-request` policy sends hello provided request toohello specified URL, waiting no longer than hello set timeout value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1f6a0-464">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-464">Policy statement</span></span>  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="1f6a0-465">Örnek</span><span class="sxs-lookup"><span data-stu-id="1f6a0-465">Example</span></span>  
 <span data-ttu-id="1f6a0-466">Bu örnek, başvuru belirteci yetkilendirme sunucusu ile tek yönlü tooverify gösterir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-466">This example shows one way tooverify a reference token with an authorization server.</span></span> <span data-ttu-id="1f6a0-467">Bu örnek hakkında daha fazla bilgi için bkz: [dış Hizmetleri'nden hello Azure API Management hizmeti kullanarak](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="1f6a0-467">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<inbound>  
  <!-- Extract Token from Authorization header parameter -->  
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />  
  
  <!-- Send request tooToken Server toovalidate token (see RFC 7662) -->  
  <send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">  
    <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>  
    <set-method>POST</set-method>  
    <set-header name="Authorization" exists-action="override">  
      <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>  
    </set-header>  
    <set-header name="Content-Type" exists-action="override">  
      <value>application/x-www-form-urlencoded</value>  
    </set-header>  
    <set-body>@($"token={(string)context.Variables["token"]}")</set-body>  
  </send-request>  
  
  <choose>  
        <!-- Check active property in response -->  
        <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">  
            <!-- Return 401 Unauthorized with http-problem payload -->  
            <return-response response-variable-name="existing response variable">  
                <set-status code="401" reason="Unauthorized" />  
                <set-header name="WWW-Authenticate" exists-action="override">  
                    <value>Bearer error="invalid_token"</value>  
                </set-header>  
            </return-response>  
        </when>  
    </choose>  
  <base />  
</inbound>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="1f6a0-468">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="1f6a0-468">Elements</span></span>  
  
|<span data-ttu-id="1f6a0-469">Öğesi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-469">Element</span></span>|<span data-ttu-id="1f6a0-470">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-470">Description</span></span>|<span data-ttu-id="1f6a0-471">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-471">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1f6a0-472">Gönderme isteği</span><span class="sxs-lookup"><span data-stu-id="1f6a0-472">send-request</span></span>|<span data-ttu-id="1f6a0-473">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-473">Root element.</span></span>|<span data-ttu-id="1f6a0-474">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-474">Yes</span></span>|  
|<span data-ttu-id="1f6a0-475">URL</span><span class="sxs-lookup"><span data-stu-id="1f6a0-475">url</span></span>|<span data-ttu-id="1f6a0-476">Merhaba isteği Hello URL'si.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-476">hello URL of hello request.</span></span>|<span data-ttu-id="1f6a0-477">Hiçbir IF modu kopyalama; = Aksi takdirde Evet.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-477">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="1f6a0-478">Yöntemi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-478">method</span></span>|<span data-ttu-id="1f6a0-479">Merhaba hello isteği için HTTP yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-479">hello HTTP method for hello request.</span></span>|<span data-ttu-id="1f6a0-480">Hiçbir IF modu kopyalama; = Aksi takdirde Evet.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-480">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="1f6a0-481">üst bilgi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-481">header</span></span>|<span data-ttu-id="1f6a0-482">İstek üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-482">Request header.</span></span> <span data-ttu-id="1f6a0-483">Birden çok üstbilgi öğeleri için birden çok istek üstbilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-483">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="1f6a0-484">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-484">No</span></span>|  
|<span data-ttu-id="1f6a0-485">Gövde</span><span class="sxs-lookup"><span data-stu-id="1f6a0-485">body</span></span>|<span data-ttu-id="1f6a0-486">Merhaba istek gövdesi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-486">hello request body.</span></span>|<span data-ttu-id="1f6a0-487">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-487">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1f6a0-488">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="1f6a0-488">Attributes</span></span>  
  
|<span data-ttu-id="1f6a0-489">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="1f6a0-489">Attribute</span></span>|<span data-ttu-id="1f6a0-490">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-490">Description</span></span>|<span data-ttu-id="1f6a0-491">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-491">Required</span></span>|<span data-ttu-id="1f6a0-492">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="1f6a0-492">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="1f6a0-493">modu = "dize"</span><span class="sxs-lookup"><span data-stu-id="1f6a0-493">mode="string"</span></span>|<span data-ttu-id="1f6a0-494">Yeni bir istek veya bir kopyasını hello geçerli istek olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-494">Determines whether this is a new request or a copy of hello current request.</span></span> <span data-ttu-id="1f6a0-495">Giden modunda modu = kopyalama hello istek gövdesi başlatamadı.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-495">In outbound mode, mode=copy does not initialize hello request body.</span></span>|<span data-ttu-id="1f6a0-496">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-496">No</span></span>|<span data-ttu-id="1f6a0-497">Yeni</span><span class="sxs-lookup"><span data-stu-id="1f6a0-497">New</span></span>|  
|<span data-ttu-id="1f6a0-498">yanıt değişkeni adı = "dize"</span><span class="sxs-lookup"><span data-stu-id="1f6a0-498">response-variable-name="string"</span></span>|<span data-ttu-id="1f6a0-499">Yoksa, `context.Response` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-499">If not present, `context.Response` is used.</span></span>|<span data-ttu-id="1f6a0-500">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-500">No</span></span>|<span data-ttu-id="1f6a0-501">Yok</span><span class="sxs-lookup"><span data-stu-id="1f6a0-501">N/A</span></span>|  
|<span data-ttu-id="1f6a0-502">zaman aşımı = "tamsayı"</span><span class="sxs-lookup"><span data-stu-id="1f6a0-502">timeout="integer"</span></span>|<span data-ttu-id="1f6a0-503">Merhaba zaman aşımı aralığı saniye hello çağrıdan önce toohello URL başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-503">hello timeout interval in seconds before hello call toohello URL fails.</span></span>|<span data-ttu-id="1f6a0-504">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-504">No</span></span>|<span data-ttu-id="1f6a0-505">60</span><span class="sxs-lookup"><span data-stu-id="1f6a0-505">60</span></span>|  
|<span data-ttu-id="1f6a0-506">Hatayı Yoksay</span><span class="sxs-lookup"><span data-stu-id="1f6a0-506">ignore-error</span></span>|<span data-ttu-id="1f6a0-507">Doğru ve hello hatayla sonuçlanır isterse:</span><span class="sxs-lookup"><span data-stu-id="1f6a0-507">If true and hello request results in an error:</span></span><br /><br /> <span data-ttu-id="1f6a0-508">-Eğer bir null değer içerecek yanıt değişkeni adı belirtildi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-508">-   If response-variable-name was specified it will contain a null value.</span></span><br /><span data-ttu-id="1f6a0-509">-Yanıt değişkeni adı belirtilmedi Eğer bağlamı. İstek güncelleştirilmez.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-509">-   If response-variable-name was not specified, context.Request will not be updated.</span></span>|<span data-ttu-id="1f6a0-510">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-510">No</span></span>|<span data-ttu-id="1f6a0-511">False</span><span class="sxs-lookup"><span data-stu-id="1f6a0-511">false</span></span>|  
|<span data-ttu-id="1f6a0-512">ad</span><span class="sxs-lookup"><span data-stu-id="1f6a0-512">name</span></span>|<span data-ttu-id="1f6a0-513">Merhaba hello üstbilgi toobe kümesinin adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-513">Specifies hello name of hello header toobe set.</span></span>|<span data-ttu-id="1f6a0-514">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-514">Yes</span></span>|<span data-ttu-id="1f6a0-515">Yok</span><span class="sxs-lookup"><span data-stu-id="1f6a0-515">N/A</span></span>|  
|<span data-ttu-id="1f6a0-516">Mevcut eylem</span><span class="sxs-lookup"><span data-stu-id="1f6a0-516">exists-action</span></span>|<span data-ttu-id="1f6a0-517">Merhaba üstbilgi zaten belirtildiğinde hangi eylemini tootake belirtir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-517">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="1f6a0-518">Bu öznitelik değerlerini aşağıdaki hello birine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-518">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="1f6a0-519">-değiştirir hello hello varolan üstbilgisinin değerini geçersiz kıl -.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-519">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="1f6a0-520">-skip - hello varolan üstbilgi değeri değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-520">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="1f6a0-521">-Ekle - hello değeri toohello varolan üstbilgi değeri ekler.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-521">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="1f6a0-522">-delete - hello üstbilgisini hello isteğinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-522">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="1f6a0-523">Ayarlandığında çok`override` birden çok girişi kaydetme; hello ile aynı sonuçları (birden çok kez listelenir) kümesi according tooall girdisi olan hello üstbilgisinde adı yalnızca listelenen değerler hello sonucunda ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-523">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="1f6a0-524">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-524">No</span></span>|<span data-ttu-id="1f6a0-525">geçersiz kılma</span><span class="sxs-lookup"><span data-stu-id="1f6a0-525">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1f6a0-526">Kullanım</span><span class="sxs-lookup"><span data-stu-id="1f6a0-526">Usage</span></span>  
 <span data-ttu-id="1f6a0-527">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1f6a0-527">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1f6a0-528">**İlke bölümleri:** gelen, giden arka uç, hata</span><span class="sxs-lookup"><span data-stu-id="1f6a0-528">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1f6a0-529">**İlke kapsamları:** tüm kapsamlar</span><span class="sxs-lookup"><span data-stu-id="1f6a0-529">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="1f6a0-530"><a name="SetHttpProxy"></a>Set HTTP proxy</span><span class="sxs-lookup"><span data-stu-id="1f6a0-530"><a name="SetHttpProxy"></a> Set HTTP proxy</span></span>  
 <span data-ttu-id="1f6a0-531">Merhaba `proxy` İlkesi tooroute iletilen istekleri toobackends bir HTTP proxy üzerinden sağlar.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-531">hello `proxy` policy allows you tooroute requests forwarded toobackends via an HTTP proxy.</span></span> <span data-ttu-id="1f6a0-532">Yalnızca HTTP (HTTPS değil) hello ağ geçidi ve hello proxy arasında desteklenir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-532">Only HTTP (not HTTPS) is supported between hello gateway and hello proxy.</span></span> <span data-ttu-id="1f6a0-533">Temel ve yalnızca NTLM kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-533">Basic and NTLM authentication only.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="1f6a0-534">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-534">Policy statement</span></span>  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="1f6a0-535">Örnek</span><span class="sxs-lookup"><span data-stu-id="1f6a0-535">Example</span></span>  
<span data-ttu-id="1f6a0-536">Not hello [özellikleri](api-management-howto-properties.md) hello İlkesi belgede hassas bilgileri depolamak hello kullanıcı adı ve parola tooavoid değerleri olarak.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-536">Note hello use of [properties](api-management-howto-properties.md) as values of hello username and password tooavoid storing sensitive information in hello policy document.</span></span>  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a><span data-ttu-id="1f6a0-537">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="1f6a0-537">Elements</span></span>  
  
|<span data-ttu-id="1f6a0-538">Öğesi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-538">Element</span></span>|<span data-ttu-id="1f6a0-539">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-539">Description</span></span>|<span data-ttu-id="1f6a0-540">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-540">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1f6a0-541">Proxy</span><span class="sxs-lookup"><span data-stu-id="1f6a0-541">proxy</span></span>|<span data-ttu-id="1f6a0-542">Kök öğesi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-542">Root element</span></span>|<span data-ttu-id="1f6a0-543">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-543">Yes</span></span>|  

### <a name="attributes"></a><span data-ttu-id="1f6a0-544">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="1f6a0-544">Attributes</span></span>  
  
|<span data-ttu-id="1f6a0-545">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="1f6a0-545">Attribute</span></span>|<span data-ttu-id="1f6a0-546">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-546">Description</span></span>|<span data-ttu-id="1f6a0-547">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-547">Required</span></span>|<span data-ttu-id="1f6a0-548">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="1f6a0-548">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="1f6a0-549">URL = "dize"</span><span class="sxs-lookup"><span data-stu-id="1f6a0-549">url="string"</span></span>|<span data-ttu-id="1f6a0-550">Proxy URL'si http://host:port hello biçiminde.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-550">Proxy URL in hello form of http://host:port.</span></span>|<span data-ttu-id="1f6a0-551">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-551">Yes</span></span>|<span data-ttu-id="1f6a0-552">Yok</span><span class="sxs-lookup"><span data-stu-id="1f6a0-552">N/A</span></span>|  
|<span data-ttu-id="1f6a0-553">Kullanıcı adı = "dize"</span><span class="sxs-lookup"><span data-stu-id="1f6a0-553">username="string"</span></span>|<span data-ttu-id="1f6a0-554">Kullanıcı adı toobe hello proxy kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-554">Username toobe used for authentication with hello proxy.</span></span>|<span data-ttu-id="1f6a0-555">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-555">No</span></span>|<span data-ttu-id="1f6a0-556">Yok</span><span class="sxs-lookup"><span data-stu-id="1f6a0-556">N/A</span></span>|  
|<span data-ttu-id="1f6a0-557">parola = "dize"</span><span class="sxs-lookup"><span data-stu-id="1f6a0-557">password="string"</span></span>|<span data-ttu-id="1f6a0-558">Parola toobe hello proxy kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-558">Password toobe used for authentication with hello proxy.</span></span>|<span data-ttu-id="1f6a0-559">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-559">No</span></span>|<span data-ttu-id="1f6a0-560">Yok</span><span class="sxs-lookup"><span data-stu-id="1f6a0-560">N/A</span></span>|  

### <a name="usage"></a><span data-ttu-id="1f6a0-561">Kullanım</span><span class="sxs-lookup"><span data-stu-id="1f6a0-561">Usage</span></span>  
 <span data-ttu-id="1f6a0-562">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1f6a0-562">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1f6a0-563">**İlke bölümleri:** gelen</span><span class="sxs-lookup"><span data-stu-id="1f6a0-563">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="1f6a0-564">**İlke kapsamları:** tüm kapsamlar</span><span class="sxs-lookup"><span data-stu-id="1f6a0-564">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="1f6a0-565"><a name="SetRequestMethod"></a>Set isteği yöntemi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-565"><a name="SetRequestMethod"></a> Set request method</span></span>  
 <span data-ttu-id="1f6a0-566">Merhaba `set-method` ilke isteği için toochange hello HTTP istek yöntemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-566">hello `set-method` policy allows you toochange hello HTTP request method for a request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1f6a0-567">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-567">Policy statement</span></span>  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a><span data-ttu-id="1f6a0-568">Örnek</span><span class="sxs-lookup"><span data-stu-id="1f6a0-568">Example</span></span>  
 <span data-ttu-id="1f6a0-569">Merhaba kullanan bu örnek ilke `set-method` ilke hello HTTP yanıt kodunu büyükse bir ileti tooa Slack sohbet odası gönderirken ya da eşit too500 örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-569">This sample policy that uses hello `set-method` policy shows an example of sending a message tooa Slack chat room if hello HTTP response code is greater than or equal too500.</span></span> <span data-ttu-id="1f6a0-570">Bu örnek hakkında daha fazla bilgi için bkz: [dış Hizmetleri'nden hello Azure API Management hizmeti kullanarak](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="1f6a0-570">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<choose>  
    <when condition="@(context.Response.StatusCode >= 500)">  
      <send-one-way-request mode="new">  
        <set-url>https://hooks.slack.com/services/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</set-url>  
        <set-method>POST</set-method>  
        <set-body>@{  
                return new JObject(  
                        new JProperty("username","APIM Alert"),  
                        new JProperty("icon_emoji", ":ghost:"),  
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",  
                                                context.Request.Method,  
                                                context.Request.Url.Path + context.Request.Url.QueryString,  
                                                context.Request.Url.Host,  
                                                context.Response.StatusCode,  
                                                context.Response.StatusReason,  
                                                context.User.Email  
                                                ))  
                        ).ToString();  
            }</set-body>  
      </send-one-way-request>  
    </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="1f6a0-571">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="1f6a0-571">Elements</span></span>  
  
|<span data-ttu-id="1f6a0-572">Öğesi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-572">Element</span></span>|<span data-ttu-id="1f6a0-573">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-573">Description</span></span>|<span data-ttu-id="1f6a0-574">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-574">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1f6a0-575">Set yöntemi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-575">set-method</span></span>|<span data-ttu-id="1f6a0-576">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-576">Root element.</span></span> <span data-ttu-id="1f6a0-577">Merhaba öğesinin Hello değeri hello HTTP yöntemini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-577">hello value of hello element specifies hello HTTP method.</span></span>|<span data-ttu-id="1f6a0-578">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-578">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1f6a0-579">Kullanım</span><span class="sxs-lookup"><span data-stu-id="1f6a0-579">Usage</span></span>  
 <span data-ttu-id="1f6a0-580">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1f6a0-580">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1f6a0-581">**İlke bölümleri:** gelen, hata</span><span class="sxs-lookup"><span data-stu-id="1f6a0-581">**Policy sections:** inbound, on-error</span></span>  
  
-   <span data-ttu-id="1f6a0-582">**İlke kapsamları:** tüm kapsamlar</span><span class="sxs-lookup"><span data-stu-id="1f6a0-582">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="1f6a0-583"><a name="SetStatus"></a>Set durum kodu</span><span class="sxs-lookup"><span data-stu-id="1f6a0-583"><a name="SetStatus"></a> Set status code</span></span>  
 <span data-ttu-id="1f6a0-584">Merhaba `set-status` ilke kümeleri hello HTTP durum kodu toohello belirtilen değeri.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-584">hello `set-status` policy sets hello HTTP status code toohello specified value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1f6a0-585">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-585">Policy statement</span></span>  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a><span data-ttu-id="1f6a0-586">Örnek</span><span class="sxs-lookup"><span data-stu-id="1f6a0-586">Example</span></span>  
 <span data-ttu-id="1f6a0-587">Bu örnekte gösterilir nasıl tooreturn hello yetkilendirme belirteci geçersiz ise 401 yanıt.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-587">This example shows how tooreturn a 401 response if hello authorization token is invalid.</span></span> <span data-ttu-id="1f6a0-588">Daha fazla bilgi için bkz: [hello Azure API Management hizmeti dış Hizmetleri'nden kullanma](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span><span class="sxs-lookup"><span data-stu-id="1f6a0-588">For more information, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span></span>  
  
```xml  
<choose>  
  <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">  
    <return-response response-variable-name="existing response variable">  
      <set-status code="401" reason="Unauthorized" />  
      <set-header name="WWW-Authenticate" exists-action="override">  
        <value>Bearer error="invalid_token"</value>  
      </set-header>  
    </return-response>  
  </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="1f6a0-589">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="1f6a0-589">Elements</span></span>  
  
|<span data-ttu-id="1f6a0-590">Öğesi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-590">Element</span></span>|<span data-ttu-id="1f6a0-591">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-591">Description</span></span>|<span data-ttu-id="1f6a0-592">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-592">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1f6a0-593">durumunu ayarla</span><span class="sxs-lookup"><span data-stu-id="1f6a0-593">set-status</span></span>|<span data-ttu-id="1f6a0-594">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-594">Root element.</span></span>|<span data-ttu-id="1f6a0-595">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-595">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1f6a0-596">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="1f6a0-596">Attributes</span></span>  
  
|<span data-ttu-id="1f6a0-597">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="1f6a0-597">Attribute</span></span>|<span data-ttu-id="1f6a0-598">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-598">Description</span></span>|<span data-ttu-id="1f6a0-599">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-599">Required</span></span>|<span data-ttu-id="1f6a0-600">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="1f6a0-600">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="1f6a0-601">kod = "tamsayı"</span><span class="sxs-lookup"><span data-stu-id="1f6a0-601">code="integer"</span></span>|<span data-ttu-id="1f6a0-602">Merhaba HTTP durum kodu tooreturn.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-602">hello HTTP status code tooreturn.</span></span>|<span data-ttu-id="1f6a0-603">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-603">Yes</span></span>|<span data-ttu-id="1f6a0-604">Yok</span><span class="sxs-lookup"><span data-stu-id="1f6a0-604">N/A</span></span>|  
|<span data-ttu-id="1f6a0-605">nedeni = "dize"</span><span class="sxs-lookup"><span data-stu-id="1f6a0-605">reason="string"</span></span>|<span data-ttu-id="1f6a0-606">Merhaba durum kodu döndürmek için hello neden açıklaması.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-606">A description of hello reason for returning hello status code.</span></span>|<span data-ttu-id="1f6a0-607">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-607">Yes</span></span>|<span data-ttu-id="1f6a0-608">Yok</span><span class="sxs-lookup"><span data-stu-id="1f6a0-608">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1f6a0-609">Kullanım</span><span class="sxs-lookup"><span data-stu-id="1f6a0-609">Usage</span></span>  
 <span data-ttu-id="1f6a0-610">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1f6a0-610">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1f6a0-611">**İlke bölümleri:** giden, arka uç, hata</span><span class="sxs-lookup"><span data-stu-id="1f6a0-611">**Policy sections:** outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1f6a0-612">**İlke kapsamları:** tüm kapsamlar</span><span class="sxs-lookup"><span data-stu-id="1f6a0-612">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="1f6a0-613"><a name="set-variable"></a>Değişken Ayarla</span><span class="sxs-lookup"><span data-stu-id="1f6a0-613"><a name="set-variable"></a> Set variable</span></span>  
 <span data-ttu-id="1f6a0-614">Hello `set-variable` İlkesi bildirir bir [bağlamı](api-management-policy-expressions.md#ContextVariables) değişkeni aracılığıyla belirtilen bir değeri atar bir [ifade](api-management-policy-expressions.md) veya bir değişmez dize değeri.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-614">hello `set-variable` policy declares a [context](api-management-policy-expressions.md#ContextVariables) variable and assigns it a value specified via an [expression](api-management-policy-expressions.md) or a string literal.</span></span> <span data-ttu-id="1f6a0-615">Merhaba ifadesi, dönüştürülmesi bir hazır değer içeriyorsa hello değerin tooa dize ve hello türü olacaktır `System.String`.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-615">if hello expression contains a literal it will be converted tooa string and hello type of hello value will be `System.String`.</span></span>  
  
###  <span data-ttu-id="1f6a0-616"><a name="set-variablePolicyStatement"></a>İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-616"><a name="set-variablePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <span data-ttu-id="1f6a0-617"><a name="set-variableExample"></a>Örnek</span><span class="sxs-lookup"><span data-stu-id="1f6a0-617"><a name="set-variableExample"></a> Example</span></span>  
 <span data-ttu-id="1f6a0-618">Merhaba aşağıdaki örnekte gösterilmiştir hello kümesi değişken ilkesinde gelen bölümü.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-618">hello following example demonstrates a set variable policy in hello inbound section.</span></span> <span data-ttu-id="1f6a0-619">Bu değişken ilkesini ayarlama oluşturur bir `isMobile` Boolean [bağlamı](api-management-policy-expressions.md#ContextVariables) tootrue hello ayarlanır değişkeni `User-Agent` istek üstbilgisi hello metni içerir `iPad` veya `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-619">This set variable policy creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set tootrue if hello `User-Agent` request header contains hello text `iPad` or `iPhone`.</span></span>  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a><span data-ttu-id="1f6a0-620">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="1f6a0-620">Elements</span></span>  
  
|<span data-ttu-id="1f6a0-621">Öğesi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-621">Element</span></span>|<span data-ttu-id="1f6a0-622">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-622">Description</span></span>|<span data-ttu-id="1f6a0-623">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-623">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1f6a0-624">değişken Ayarla</span><span class="sxs-lookup"><span data-stu-id="1f6a0-624">set-variable</span></span>|<span data-ttu-id="1f6a0-625">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-625">Root element.</span></span>|<span data-ttu-id="1f6a0-626">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-626">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1f6a0-627">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="1f6a0-627">Attributes</span></span>  
  
|<span data-ttu-id="1f6a0-628">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="1f6a0-628">Attribute</span></span>|<span data-ttu-id="1f6a0-629">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-629">Description</span></span>|<span data-ttu-id="1f6a0-630">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-630">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="1f6a0-631">ad</span><span class="sxs-lookup"><span data-stu-id="1f6a0-631">name</span></span>|<span data-ttu-id="1f6a0-632">Merhaba değişkeninin Hello adı.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-632">hello name of hello variable.</span></span>|<span data-ttu-id="1f6a0-633">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-633">Yes</span></span>|  
|<span data-ttu-id="1f6a0-634">değer</span><span class="sxs-lookup"><span data-stu-id="1f6a0-634">value</span></span>|<span data-ttu-id="1f6a0-635">Merhaba değişkenin Hello değeri.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-635">hello value of hello variable.</span></span> <span data-ttu-id="1f6a0-636">Bu bir deyim veya bir hazır değer olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-636">This can be an expression or a literal value.</span></span>|<span data-ttu-id="1f6a0-637">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-637">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1f6a0-638">Kullanım</span><span class="sxs-lookup"><span data-stu-id="1f6a0-638">Usage</span></span>  
 <span data-ttu-id="1f6a0-639">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1f6a0-639">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1f6a0-640">**İlke bölümleri:** gelen, giden arka uç, hata</span><span class="sxs-lookup"><span data-stu-id="1f6a0-640">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1f6a0-641">**İlke kapsamları:** tüm kapsamlar</span><span class="sxs-lookup"><span data-stu-id="1f6a0-641">**Policy scopes:** all scopes</span></span>  
  
###  <span data-ttu-id="1f6a0-642"><a name="set-variableAllowedTypes"></a>İzin verilen türleri</span><span class="sxs-lookup"><span data-stu-id="1f6a0-642"><a name="set-variableAllowedTypes"></a> Allowed types</span></span>  
 <span data-ttu-id="1f6a0-643">Hello kullanılan ifadeleri `set-variable` İlkesi şu temel türlerini hello birini döndürmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-643">Expressions used in hello `set-variable` policy must return one of hello following basic types.</span></span>  
  
-   <span data-ttu-id="1f6a0-644">System.Boolean</span><span class="sxs-lookup"><span data-stu-id="1f6a0-644">System.Boolean</span></span>  
  
-   <span data-ttu-id="1f6a0-645">System.SByte</span><span class="sxs-lookup"><span data-stu-id="1f6a0-645">System.SByte</span></span>  
  
-   <span data-ttu-id="1f6a0-646">System.Byte</span><span class="sxs-lookup"><span data-stu-id="1f6a0-646">System.Byte</span></span>  
  
-   <span data-ttu-id="1f6a0-647">System.UInt16</span><span class="sxs-lookup"><span data-stu-id="1f6a0-647">System.UInt16</span></span>  
  
-   <span data-ttu-id="1f6a0-648">System.UInt32</span><span class="sxs-lookup"><span data-stu-id="1f6a0-648">System.UInt32</span></span>  
  
-   <span data-ttu-id="1f6a0-649">System.UInt64</span><span class="sxs-lookup"><span data-stu-id="1f6a0-649">System.UInt64</span></span>  
  
-   <span data-ttu-id="1f6a0-650">System.Int16</span><span class="sxs-lookup"><span data-stu-id="1f6a0-650">System.Int16</span></span>  
  
-   <span data-ttu-id="1f6a0-651">System.Int32</span><span class="sxs-lookup"><span data-stu-id="1f6a0-651">System.Int32</span></span>  
  
-   <span data-ttu-id="1f6a0-652">System.Int64</span><span class="sxs-lookup"><span data-stu-id="1f6a0-652">System.Int64</span></span>  
  
-   <span data-ttu-id="1f6a0-653">System.Decimal</span><span class="sxs-lookup"><span data-stu-id="1f6a0-653">System.Decimal</span></span>  
  
-   <span data-ttu-id="1f6a0-654">System.Single</span><span class="sxs-lookup"><span data-stu-id="1f6a0-654">System.Single</span></span>  
  
-   <span data-ttu-id="1f6a0-655">System.Double</span><span class="sxs-lookup"><span data-stu-id="1f6a0-655">System.Double</span></span>  
  
-   <span data-ttu-id="1f6a0-656">System.Guid</span><span class="sxs-lookup"><span data-stu-id="1f6a0-656">System.Guid</span></span>  
  
-   <span data-ttu-id="1f6a0-657">System.String</span><span class="sxs-lookup"><span data-stu-id="1f6a0-657">System.String</span></span>  
  
-   <span data-ttu-id="1f6a0-658">System.Char</span><span class="sxs-lookup"><span data-stu-id="1f6a0-658">System.Char</span></span>  
  
-   <span data-ttu-id="1f6a0-659">System.DateTime</span><span class="sxs-lookup"><span data-stu-id="1f6a0-659">System.DateTime</span></span>  
  
-   <span data-ttu-id="1f6a0-660">System.TimeSpan</span><span class="sxs-lookup"><span data-stu-id="1f6a0-660">System.TimeSpan</span></span>  
  
-   <span data-ttu-id="1f6a0-661">System.Byte?</span><span class="sxs-lookup"><span data-stu-id="1f6a0-661">System.Byte?</span></span>  
  
-   <span data-ttu-id="1f6a0-662">System.UInt16?</span><span class="sxs-lookup"><span data-stu-id="1f6a0-662">System.UInt16?</span></span>  
  
-   <span data-ttu-id="1f6a0-663">System.UInt32?</span><span class="sxs-lookup"><span data-stu-id="1f6a0-663">System.UInt32?</span></span>  
  
-   <span data-ttu-id="1f6a0-664">System.UInt64?</span><span class="sxs-lookup"><span data-stu-id="1f6a0-664">System.UInt64?</span></span>  
  
-   <span data-ttu-id="1f6a0-665">System.Int16?</span><span class="sxs-lookup"><span data-stu-id="1f6a0-665">System.Int16?</span></span>  
  
-   <span data-ttu-id="1f6a0-666">System.Int32?</span><span class="sxs-lookup"><span data-stu-id="1f6a0-666">System.Int32?</span></span>  
  
-   <span data-ttu-id="1f6a0-667">System.Int64?</span><span class="sxs-lookup"><span data-stu-id="1f6a0-667">System.Int64?</span></span>  
  
-   <span data-ttu-id="1f6a0-668">System.Decimal?</span><span class="sxs-lookup"><span data-stu-id="1f6a0-668">System.Decimal?</span></span>  
  
-   <span data-ttu-id="1f6a0-669">System.Single?</span><span class="sxs-lookup"><span data-stu-id="1f6a0-669">System.Single?</span></span>  
  
-   <span data-ttu-id="1f6a0-670">System.Double?</span><span class="sxs-lookup"><span data-stu-id="1f6a0-670">System.Double?</span></span>  
  
-   <span data-ttu-id="1f6a0-671">System.Guid?</span><span class="sxs-lookup"><span data-stu-id="1f6a0-671">System.Guid?</span></span>  
  
-   <span data-ttu-id="1f6a0-672">System.String?</span><span class="sxs-lookup"><span data-stu-id="1f6a0-672">System.String?</span></span>  
  
-   <span data-ttu-id="1f6a0-673">System.Char?</span><span class="sxs-lookup"><span data-stu-id="1f6a0-673">System.Char?</span></span>  
  
-   <span data-ttu-id="1f6a0-674">System.DateTime?</span><span class="sxs-lookup"><span data-stu-id="1f6a0-674">System.DateTime?</span></span>  

##  <span data-ttu-id="1f6a0-675"><a name="Trace"></a>İzleme</span><span class="sxs-lookup"><span data-stu-id="1f6a0-675"><a name="Trace"></a> Trace</span></span>  
 <span data-ttu-id="1f6a0-676">Merhaba `trace` İlkesi hello bir dize ekler [API denetçisi](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) çıktı.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-676">hello             `trace` policy adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span> <span data-ttu-id="1f6a0-677">Hello ilkesi yalnızca, izleme, yani tetiklenir yürütecek `Ocp-Apim-Trace` istek üstbilgisi varsa ve çok`true` ve `Ocp-Apim-Subscription-Key` istek üstbilgisi bulunduğundan ve hello yönetici hesabıyla ilişkilendirilmiş geçerli bir anahtar tutar.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-677">hello policy will execute only when tracing is triggered, i.e. `Ocp-Apim-Trace` request header is present and set too`true` and `Ocp-Apim-Subscription-Key` request header is present and holds a valid key associated with hello admin account.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1f6a0-678">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-678">Policy statement</span></span>  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="1f6a0-679">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="1f6a0-679">Elements</span></span>  
  
|<span data-ttu-id="1f6a0-680">Öğesi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-680">Element</span></span>|<span data-ttu-id="1f6a0-681">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-681">Description</span></span>|<span data-ttu-id="1f6a0-682">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-682">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1f6a0-683">İzleme</span><span class="sxs-lookup"><span data-stu-id="1f6a0-683">trace</span></span>|<span data-ttu-id="1f6a0-684">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-684">Root element.</span></span>|<span data-ttu-id="1f6a0-685">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-685">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1f6a0-686">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="1f6a0-686">Attributes</span></span>  
  
|<span data-ttu-id="1f6a0-687">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="1f6a0-687">Attribute</span></span>|<span data-ttu-id="1f6a0-688">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-688">Description</span></span>|<span data-ttu-id="1f6a0-689">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-689">Required</span></span>|<span data-ttu-id="1f6a0-690">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="1f6a0-690">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="1f6a0-691">Kaynak</span><span class="sxs-lookup"><span data-stu-id="1f6a0-691">source</span></span>|<span data-ttu-id="1f6a0-692">Dize değişmez değer anlamlı toohello izleme Görüntüleyicisi'ni ve belirten hello kaynağı hello iletisi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-692">String literal meaningful toohello trace viewer and specifying hello source of hello message.</span></span>|<span data-ttu-id="1f6a0-693">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-693">Yes</span></span>|<span data-ttu-id="1f6a0-694">Yok</span><span class="sxs-lookup"><span data-stu-id="1f6a0-694">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1f6a0-695">Kullanım</span><span class="sxs-lookup"><span data-stu-id="1f6a0-695">Usage</span></span>  
 <span data-ttu-id="1f6a0-696">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="1f6a0-696">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="1f6a0-697">**İlke bölümleri:** gelen, giden arka uç, hata</span><span class="sxs-lookup"><span data-stu-id="1f6a0-697">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1f6a0-698">**İlke kapsamları:** tüm kapsamlar</span><span class="sxs-lookup"><span data-stu-id="1f6a0-698">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="1f6a0-699"><a name="Wait"></a>Bekleme</span><span class="sxs-lookup"><span data-stu-id="1f6a0-699"><a name="Wait"></a> Wait</span></span>  
 <span data-ttu-id="1f6a0-700">Merhaba `wait` ilke hemen alt ilkelerine paralel olarak yürütür ve tamamlanmadan önce tüm ya da kendi hemen alt ilkeleri toocomplete biri için bekler.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-700">hello `wait` policy executes its immediate child policies in parallel, and waits for either all or one of its immediate child policies toocomplete before it completes.</span></span> <span data-ttu-id="1f6a0-701">Merhaba bekleme ilke hemen alt ilkelerine olabilir [gönderme isteği](api-management-advanced-policies.md#SendRequest), [değeri önbellekten alma](api-management-caching-policies.md#GetFromCacheByKey), ve [kontrol akışı](api-management-advanced-policies.md#choose) ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-701">hello wait policy can have as its immediate child policies [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), and [Control flow](api-management-advanced-policies.md#choose) policies.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1f6a0-702">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-702">Policy statement</span></span>  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a><span data-ttu-id="1f6a0-703">Örnek</span><span class="sxs-lookup"><span data-stu-id="1f6a0-703">Example</span></span>  
 <span data-ttu-id="1f6a0-704">Aşağıdaki örneğine hello vardır iki `choose` ilkeleri hello hemen alt ilkelerini olarak `wait` ilkesi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-704">In hello following example there are two `choose` policies as immediate child policies of hello `wait` policy.</span></span> <span data-ttu-id="1f6a0-705">Bunların her biri `choose` ilkeleri paralel olarak yürütür.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-705">Each of these `choose` policies executes in parallel.</span></span> <span data-ttu-id="1f6a0-706">Her `choose` İlkesi, bir önbelleğe alınan değer tooretrieve çalışır.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-706">Each `choose` policy attempts tooretrieve a cached value.</span></span> <span data-ttu-id="1f6a0-707">Önbellek isabetsizliği varsa, arka uç hizmeti tooprovide hello değer adı verilir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-707">If there is a cache miss, a backend service is called tooprovide hello value.</span></span> <span data-ttu-id="1f6a0-708">Bu örnek hello içinde `wait` İlkesi tamamlamaz hemen alt ilkeler tamamlanana kadar çünkü hello `for` özniteliği olarak ayarlanmış çok`all`.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-708">In this example hello `wait` policy does not complete until all of its immediate child policies complete, because hello `for` attribute is set too`all`.</span></span>   <span data-ttu-id="1f6a0-709">Bu örnek hello bağlam değişkenlerine (`execute-branch-one`, `value-one`, `execute-branch-two`, ve `value-two`) Bu örnek ilke hello kapsamı dışında bildirilir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-709">In this example hello context variables (`execute-branch-one`, `value-one`, `execute-branch-two`, and `value-two`) are declared outside of hello scope of this example policy.</span></span>  
  
```xml  
<wait for="all">  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-one="])">  
      <cache-lookup-value key="key-one" variable-name="value-one" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-one="))">  
          <send-request mode="new" response-variable-name="value-one">  
            <set-url>https://backend-one</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-two="])">  
      <cache-lookup-value key="key-two" variable-name="value-two" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-two="))">  
          <send-request mode="new" response-variable-name="value-two">  
            <set-url>https://backend-two</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
</wait>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="1f6a0-710">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="1f6a0-710">Elements</span></span>  
  
|<span data-ttu-id="1f6a0-711">Öğesi</span><span class="sxs-lookup"><span data-stu-id="1f6a0-711">Element</span></span>|<span data-ttu-id="1f6a0-712">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-712">Description</span></span>|<span data-ttu-id="1f6a0-713">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-713">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1f6a0-714">bekleme</span><span class="sxs-lookup"><span data-stu-id="1f6a0-714">wait</span></span>|<span data-ttu-id="1f6a0-715">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-715">Root element.</span></span> <span data-ttu-id="1f6a0-716">Yalnızca alt öğeleri içerebilir `send-request`, `cache-lookup-value`, ve `choose` ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-716">May contain as child elements only `send-request`, `cache-lookup-value`, and `choose` policies.</span></span>|<span data-ttu-id="1f6a0-717">Evet</span><span class="sxs-lookup"><span data-stu-id="1f6a0-717">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1f6a0-718">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="1f6a0-718">Attributes</span></span>  
  
|<span data-ttu-id="1f6a0-719">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="1f6a0-719">Attribute</span></span>|<span data-ttu-id="1f6a0-720">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f6a0-720">Description</span></span>|<span data-ttu-id="1f6a0-721">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1f6a0-721">Required</span></span>|<span data-ttu-id="1f6a0-722">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="1f6a0-722">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="1f6a0-723">için</span><span class="sxs-lookup"><span data-stu-id="1f6a0-723">for</span></span>|<span data-ttu-id="1f6a0-724">Hello olup olmadığını belirleyen `wait` İlkesi bekler tamamlandı tüm hemen alt ilkeleri toobe için veya tek bir.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-724">Determines whether hello `wait` policy waits for all immediate child policies toobe completed or just one.</span></span> <span data-ttu-id="1f6a0-725">İzin verilen değerler:</span><span class="sxs-lookup"><span data-stu-id="1f6a0-725">Allowed values are:</span></span><br /><br /> <span data-ttu-id="1f6a0-726">-   `all`-Tüm hemen alt ilkeleri toocomplete için bekleyin</span><span class="sxs-lookup"><span data-stu-id="1f6a0-726">-   `all` - wait for all immediate child policies toocomplete</span></span><br /><span data-ttu-id="1f6a0-727">-any - tüm hemen alt ilke toocomplete için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-727">-   any - wait for any immediate child policy toocomplete.</span></span> <span data-ttu-id="1f6a0-728">Merhaba ilk hemen alt ilke tamamlandıktan sonra hello `wait` ilkeyi tamamladıktan ve diğer hemen alt ilkeleri yürütülmesi biter.</span><span class="sxs-lookup"><span data-stu-id="1f6a0-728">Once hello first immediate child policy has completed, hello `wait` policy completes and execution of any other immediate child policies is terminated.</span></span>|<span data-ttu-id="1f6a0-729">Hayır</span><span class="sxs-lookup"><span data-stu-id="1f6a0-729">No</span></span>|<span data-ttu-id="1f6a0-730">Tüm</span><span class="sxs-lookup"><span data-stu-id="1f6a0-730">all</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1f6a0-731">Kullanım</span><span class="sxs-lookup"><span data-stu-id="1f6a0-731">Usage</span></span>  
 <span data-ttu-id="1f6a0-732">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1f6a0-732">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1f6a0-733">**İlke bölümleri:** gelen, giden arka uç</span><span class="sxs-lookup"><span data-stu-id="1f6a0-733">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="1f6a0-734">**İlke kapsamları:**tüm kapsamlar</span><span class="sxs-lookup"><span data-stu-id="1f6a0-734">**Policy scopes:**all scopes</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="1f6a0-735">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1f6a0-735">Next steps</span></span>
<span data-ttu-id="1f6a0-736">İlkeleriyle çalışma daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="1f6a0-736">For more information working with policies, see:</span></span>
-   [<span data-ttu-id="1f6a0-737">API Management ilkeleri</span><span class="sxs-lookup"><span data-stu-id="1f6a0-737">Policies in API Management</span></span>](api-management-howto-policies.md) 
-   [<span data-ttu-id="1f6a0-738">İlke ifadeleri</span><span class="sxs-lookup"><span data-stu-id="1f6a0-738">Policy expressions</span></span>](api-management-policy-expressions.md)
