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
# <a name="api-management-caching-policies"></a>API Management önbelleğe alma ilkeleri
Bu konuda API Management ilkelere hello için bir başvuru sağlar. Ekleme ve ilkeleri yapılandırma hakkında daha fazla bilgi için bkz: [API Management ilkeleri](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="CachingPolicies"></a>Önbelleğe alma ilkeleri  
  
-   Yanıt önbelleğe alma ilkeleri  
  
    -   [Önbellekten alma](api-management-caching-policies.md#GetFromCache) -önbellek gerçekleştirmek aramak ve geçerli bir önbelleğe alınan yanıtları kullanılabilir olduğunda döndürür.  
  
    -   [Depolama toocache](api-management-caching-policies.md#StoreToCache) - toohello belirtilen önbellek denetimi yapılandırma göre önbellekleri yanıtlar.  
  
-   Değer önbelleğe alma ilkeleri  
  
    -   [Önbelleğe alınan değer alma](#GetFromCacheByKey) -anahtar tarafından önbelleğe alınmış bir öğeyi geri almak.  
  
    -   [Değer önbellekte depolamak](#StoreToCacheByKey) -bir öğe anahtarı tarafından hello önbelleğine depolayabilirsiniz.  
  
    -   [Önbelleğe alınan değer Kaldır](#RemoveCacheByKey) -öğeyi hello önbelleğinde anahtarının kaldırmak.  
  
##  <a name="GetFromCache"></a>Önbellekten alma  
 Kullanım hello `cache-lookup` ilke tooperform önbelleği aramak ve geçerli bir önbelleğe alınan yanıt kullanılabilir olduğunda döndürür. Bu ilke, yanıt içeriği bir süre boyunca statik kalır olduğu durumlarda uygulanabilir. Yanıt önbelleğe alma bant genişliğini azaltır ve işleme gereksinimlerini gecikmede API tüketiciler tarafından algılanan hello arka uç web sunucusu ve düşürmeye uygulanmaz.  
  
> [!NOTE]
>  Bu ilke karşılık gelen olmalıdır [deposu toocache](api-management-caching-policies.md#StoreToCache) ilkesi.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
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
  
### <a name="examples"></a>Örnekler  
  
#### <a name="example"></a>Örnek  
  
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
  
#### <a name="example-using-policy-expressions"></a>Örnek ilke ifadeleri kullanma  
 Bu örnek, hizmetin nasıl tootooconfigure API Management yanıt önbelleğe alma süresi eşleşmeleri hello belirtildiği gibi hello arka uç hizmetinin yanıt önbelleğe alma hello yedeklenen gösterir `Cache-Control` yönergesi. Yapılandırma ve bu ilkeyi kullanan bir örnek için bkz: [bulut kapak bölüm 177: daha Vlad Vinogradsky ile yönetim özelliklerini API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) ve too25:25 ileri sarma.  
  
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
  
 Daha fazla bilgi için bkz: [ilke ifadelerini](api-management-policy-expressions.md) ve [bağlamının](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="elements"></a>Öğeleri  
  
|Ad|Açıklama|Gerekli|  
|----------|-----------------|--------------|  
|Önbellek araması|Kök öğesi.|Evet|  
|farklılık tarafından-üstbilgisi|Ana bilgisayardan kabul, Accept-Charset, Accept-Encoding, Accept-Language, yetkilendirme gibi Expect, belirtilen üstbilgi değerini başına yanıtlarını önbelleğe alma Başlat IF-Match.|Hayır|  
|farklılık-tarafından-query-parametresi|Her değeri belirtilen sorgu parametrelerinin yanıtlarını önbelleğe alma başlatın. Tek bir veya birden çok parametre girin. Ayırıcı olarak virgül kullanın. Hiçbiri belirtilmezse, tüm sorgu parametreleri kullanılır.|Hayır|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Ad|Açıklama|Gerekli|Varsayılan|  
|----------|-----------------|--------------|-------------|  
|izin ver-özel-yanıt-önbelleğe alma|Ayarlandığında çok`true`, bir Authorization üstbilgisi içeren istekleri önbelleğe alma sağlar.|Hayır|False|  
|önbelleğe alma aşağı akış türü|Bu öznitelik değerlerini aşağıdaki hello tooone ayarlamanız gerekir.<br /><br /> -none - aşağı akış önbelleğe alma izin verilmez.<br />-Özel - aşağı akış özel önbelleğe alma izin verilir.<br />-Genel - özel ve paylaşılan aşağı akış önbelleğe alma izin verilir.|Hayır|Yok|  
|gereken revalidate|Aşağı Akış önbelleği etkin olduğunda, bu öznitelik açar veya hello kapatır `must-revalidate` ağ geçidi yanıtlarındaki önbellek denetimi yönergesi.|Hayır|TRUE|  
|farklılık-tarafından-Geliştirici|Çok ayarlamak`true` Geliştirici anahtar başına toocache yanıtlar.|Hayır|False|  
|farklılık tarafından-Geliştirici-grupları|Çok ayarlamak`true` kullanıcı rol başına toocache yanıtlar.|Hayır|False|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen  
  
-   **İlke kapsamları:** API işlemi, ürün  
  
##  <a name="StoreToCache"></a>Depolama toocache  
 Merhaba `cache-store` toohello göre ilke önbellekleri yanıtları belirtilen önbellek ayarları. Bu ilke, yanıt içeriği bir süre boyunca statik kalır olduğu durumlarda uygulanabilir. Yanıt önbelleğe alma bant genişliğini azaltır ve işleme gereksinimlerini gecikmede API tüketiciler tarafından algılanan hello arka uç web sunucusu ve düşürmeye uygulanmaz.  
  
> [!NOTE]
>  Bu ilke karşılık gelen olmalıdır [önbellekten alma](api-management-caching-policies.md#GetFromCache) ilkesi.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a>Örnekler  
  
#### <a name="example"></a>Örnek  
  
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
  
#### <a name="example-using-policy-expressions"></a>Örnek ilke ifadeleri kullanma  
 Bu örnek, hizmetin nasıl tootooconfigure API Management yanıt önbelleğe alma süresi eşleşmeleri hello belirtildiği gibi hello arka uç hizmetinin yanıt önbelleğe alma hello yedeklenen gösterir `Cache-Control` yönergesi. Yapılandırma ve bu ilkeyi kullanan bir örnek için bkz: [bulut kapak bölüm 177: daha Vlad Vinogradsky ile yönetim özelliklerini API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) ve too25:25 ileri sarma.  
  
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
  
 Daha fazla bilgi için bkz: [ilke ifadelerini](api-management-policy-expressions.md) ve [bağlamının](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="elements"></a>Öğeleri  
  
|Ad|Açıklama|Gerekli|  
|----------|-----------------|--------------|  
|Önbellek deposu|Kök öğesi.|Evet|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Ad|Açıklama|Gerekli|Varsayılan|  
|----------|-----------------|--------------|-------------|  
|Süre|Time-to-live Merhaba, saniye cinsinden belirtilen girişleri, önbelleğe alınmış.|Evet|Yok|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** giden  
  
-   **İlke kapsamları:** API işlemi, ürün  
  
##  <a name="GetFromCacheByKey"></a>Önbelleğe alınan değer alma  
 Kullanım hello `cache-lookup-value` İlkesi tooperform arama anahtar tarafından önbelleğe ve önbelleğe alınan değeri döndürür. Merhaba anahtar bir isteğe bağlı bir dize değerine sahip olabilir ve genellikle bir ilke ifade kullanılarak sağlanır.  
  
> [!NOTE]
>  Bu ilke karşılık gelen olmalıdır [değeri önbellekte depolamak](#StoreToCacheByKey) ilkesi.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value toouse if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a>Örnek  
 Daha fazla bilgi ve bu ilkeyi örnekleri için bkz: [özel Azure API Management'te önbelleğe alma](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a>Öğeleri  
  
|Ad|Açıklama|Gerekli|  
|----------|-----------------|--------------|  
|Önbellek arama değeri|Kök öğesi.|Evet|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Ad|Açıklama|Gerekli|Varsayılan|  
|----------|-----------------|--------------|-------------|  
|Varsayılan değer|Merhaba önbellek anahtar arama bir isabetsizliği oluştuysa toohello değişkeni atanacak bir değer. Bu özniteliği belirtilmezse, `null` atanır.|Hayır|`null`|  
|anahtar|Anahtar değeri toouse hello aramada önbelleğe alır.|Evet|Yok|  
|değişken adı|Merhaba adını [bağlamının](api-management-policy-expressions.md#ContextVariables) değeri Aranan hello atanacak için arama başarılı olduğunda. Arama bir isabetsizliği sonuçlanırsa hello değişkeni hello hello değeri atanacak `default-value` özniteliği veya `null`Merhaba, `default-value` özniteliği atlanmış.|Evet|Yok|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen, giden arka uç, hata  
  
-   **İlke kapsamları:** Genel API, işlemi, ürünü  
  
##  <a name="StoreToCacheByKey"></a>Önbellek deposu değeri  
 Merhaba `cache-store-value` önbellek depolama anahtarının gerçekleştirir. Merhaba anahtar bir isteğe bağlı bir dize değerine sahip olabilir ve genellikle bir ilke ifade kullanılarak sağlanır.  
  
> [!NOTE]
>  Bu ilke karşılık gelen olmalıdır [değeri önbellekten alma](#GetFromCacheByKey) ilkesi.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<cache-store-value key="cache key value" value="value toocache" duration="seconds" />  
```  
  
### <a name="example"></a>Örnek  
 Daha fazla bilgi ve bu ilkeyi örnekleri için bkz: [özel Azure API Management'te önbelleğe alma](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a>Öğeleri  
  
|Ad|Açıklama|Gerekli|  
|----------|-----------------|--------------|  
|Önbellek deposu değeri|Kök öğesi.|Evet|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Ad|Açıklama|Gerekli|Varsayılan|  
|----------|-----------------|--------------|-------------|  
|Süre|Saniye cinsinden belirtilen süre değerinin sağlanan hello için değer önbelleğe alınır.|Evet|Yok|  
|anahtar|Önbellek anahtar hello değeri altında depolanır.|Evet|Yok|  
|değer|Merhaba değeri toobe önbelleğe alınmış.|Evet|Yok|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen, giden arka uç, hata  
  
-   **İlke kapsamları:** Genel API, işlemi, ürünü  
  
###  <a name="RemoveCacheByKey"></a>Önbelleğe alınan değer Kaldır  
 Merhaba `cache-remove-value` anahtara göre tanımlanan önbelleğe alınmış bir öğeyi siler. Merhaba anahtar bir isteğe bağlı bir dize değerine sahip olabilir ve genellikle bir ilke ifade kullanılarak sağlanır.  
  
#### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a>Örnek  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a>Öğeleri  
  
|Ad|Açıklama|Gerekli|  
|----------|-----------------|--------------|  
|Önbellek Kaldır değeri|Kök öğesi.|Evet|  
  
#### <a name="attributes"></a>Öznitelikler  
  
|Ad|Açıklama|Gerekli|Varsayılan|  
|----------|-----------------|--------------|-------------|  
|anahtar|Merhaba Hello anahtarı değeri toobe hello önbellekten kaldırıldı daha önce önbelleğe alınmış.|Evet|Yok|  
  
#### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .  
  
-   **İlke bölümleri:** gelen, giden arka uç, hata  
  
-   **İlke kapsamları:** Genel API, işlemi, ürünü  
  

## <a name="next-steps"></a>Sonraki adımlar
İlkeleriyle çalışma daha fazla bilgi için bkz: [API Management ilkeleri](api-management-howto-policies.md).  