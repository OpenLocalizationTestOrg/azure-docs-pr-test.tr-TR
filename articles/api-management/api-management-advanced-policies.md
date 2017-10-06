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
# <a name="api-management-advanced-policies"></a>API Management ilkeleri Gelişmiş
Bu konuda API Management ilkelere hello için bir başvuru sağlar. Ekleme ve ilkeleri yapılandırma hakkında daha fazla bilgi için bkz: [API Management ilkeleri](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="AdvancedPolicies"></a>Gelişmiş ilkeleri  
  
-   [Denetim akışı](api-management-advanced-policies.md#choose) - koşullu ilke deyimleri hello hello değerlendirme Boole sonuçlarına dayalı uygular [ifadeleri](api-management-policy-expressions.md).  
  
-   [İstek](#ForwardRequest) -hello isteği toohello arka uç hizmeti iletir.

-   [Eşzamanlılık sınırlamak](#LimitConcurrency) -engeller içine tarafından belirtilen istek sayısının aynı anda hello fazlasını yürütülmesini ilkeleri.
  
-   [TooEvent Hub oturum](#log-to-eventhub) -hello gönderdiği iletileri belirtilen olay hub'ı Günlükçü varlık tarafından tanımlanan biçimi tooan. 

-   [Yanıt mock](#mock-response) -iptalleri potansiyel satış, yürütme ve mocked bir yanıt döndürür doğrudan toohello çağıran.
  
-   [Yeniden deneme](#Retry) -hello yürütülmesi yeniden deneme içine ilke deyimleri varsa ve hello koşul yerine getirilene kadar. Yürütme yineleyin belirtilen zaman aralığı hello ve belirtilen toohello yeniden deneme sayısı.  
  
-   [Yanıt](#ReturnResponse) -iptalleri ardışık düzen yürütmesi ve döndürür hello belirtilen yanıt doğrudan toohello çağıran. 
  
-   [Tek yönlü İsteği Gönder](#SendOneWayRequest) -bir istek toohello belirtilen URL için bir yanıt beklemeden gönderir.  
  
-   [İsteği Gönder](#SendRequest) -bir istek toohello belirtilen URL gönderir.  

-   [HTTP proxy ayarlamak](#SetHttpProxy) -bir HTTP proxy üzerinden iletilen tooroute isteklere izin verir.  

-   [İstek yöntemini ayarla](#SetRequestMethod) -bir istek için toochange hello HTTP yöntemi sağlar.  
  
-   [Durum kodu ayarlamak](#SetStatus) -değişiklikleri hello HTTP durum kodu toohello belirtilen değeri.  
  
-   [Değişken Ayarla](api-management-advanced-policies.md#set-variable) -adlandırılmış bir değer devam [bağlamı](api-management-policy-expressions.md#ContextVariables) sonraki erişim için değişken.  

-   [İzleme](#Trace) -hello bir dize ekler [API denetçisi](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) çıktı.  
  
-   [Bekleyin](#Wait) -içine için bekleyeceği [gönderme isteği](api-management-advanced-policies.md#SendRequest), [değeri önbellekten alma](api-management-caching-policies.md#GetFromCacheByKey), veya [kontrol akışı](api-management-advanced-policies.md#choose) ilkeleri toocomplete devam etmeden önce.  
  
##  <a name="choose"></a>Denetim akışı  
 Merhaba `choose` ilke ifadeleri değerlendirme Boole ifadeleri, benzer tooan IF-then-else veya bir anahtar hello sonucunu temel alarak bir programlama dilinde oluşturmak iliştirilmiş ilke uygulanır.  
  
###  <a name="ChoosePolicyStatement"></a>İlke bildirimi  
  
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
  
 Merhaba denetim akışı ilke en az birini içermelidir `<when/>` öğesi. Merhaba `<otherwise/>` öğesidir isteğe bağlıdır. Koşulları `<when/>` öğeleri sırasına görünümlerini hello ilke içinde değerlendirilir. İlke deyim Hello içinde ilk içine `<when/>` koşul özniteliği eşittir öğeyle `true` uygulanır. İçinde Hello içine ilkeleri `<otherwise/>` öğesi, varsa, tüm uygulanacak Merhaba, `<when/>` öğesi koşul öznitelikleri `false`.  
  
### <a name="examples"></a>Örnekler  
  
####  <a name="ChooseExample"></a>Örnek  
 Merhaba aşağıdaki örnekte gösterilmiştir bir [değişken Ayarla](api-management-advanced-policies.md#set-variable) İlkesi ve iki denetim akışı ilkeleri.  
  
 gelen bölüm hello ve oluşturur Hello değişken ilkesini ayarlama zamanı bir `isMobile` Boolean [bağlamı](api-management-policy-expressions.md#ContextVariables) tootrue hello ayarlanır değişkeni `User-Agent` istek üstbilgisi hello metni içerir `iPad` veya `iPhone`.  
  
 Merhaba ilk denetim akışı ilke konusu de gelen bölüm hello ve koşullu iki biri geçerlidir [ayarlamak sorgu dizesi parametresi](api-management-transformation-policies.md#SetQueryStringParameter) hello hello değerine bağlı olarak ilkeleri `isMobile` bağlamının.  
  
 Merhaba ikinci denetim akışı ilke hello giden bölümünde ve koşullu hello geçerlidir [Dönüştür XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) İlkesi zaman `isMobile` çok ayarlanır`true`.  
  
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
  
#### <a name="example"></a>Örnek  
 Bu örnek nasıl hello yanıttan veri öğeleri kaldırarak tooperform içerik filtreleme hello arka uç hizmetinden hello kullanırken alınan gösterir `Starter` ürün. Yapılandırma ve bu ilkeyi kullanan bir örnek için bkz: [bulut kapak bölüm 177: daha Vlad Vinogradsky ile yönetim özelliklerini API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) ve too34:30 ileri sarma. Genel bir bakış 31:50 toosee Başlat [koyu Sky tahmin API hello](https://developer.forecast.io/) bu tanıtım için kullanılır.  
  
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
  
### <a name="elements"></a>Öğeleri  
  
|Öğesi|Açıklama|Gerekli|  
|-------------|-----------------|--------------|  
|seçin|Kök öğesi.|Evet|  
|ne zaman|Koşul toouse hello için hello `if` veya `ifelse` hello bölümlerini `choose` ilkesi. Merhaba, `choose` ilkesine sahip birden çok `when` bölümler, sıralı olarak değerlendirilir. Bir kez hello `condition` olduğunda öğesi çok değerlendirir`true`, daha fazla `when` koşullar değerlendirilir.|Evet|  
|Aksi takdirde|Merhaba hiçbiri kullanılan hello İlkesi parçacığı toobe içeren `when` koşulları değerlendirin çok`true`.|Hayır|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Öznitelik|Açıklama|Gerekli|  
|---------------|-----------------|--------------|  
|koşul = "Boole ifadesi &#124; Boole sabiti"|Merhaba Boole ifadesi veya ne zaman içeren hello sabit tooevaluated `when` ilke bildirimi değerlendirildiği.|Evet|  
  
###  <a name="ChooseUsage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen, giden arka uç, hata  
  
-   **İlke kapsamları:** tüm kapsamlar  
  
##  <a name="ForwardRequest"></a>İstek  
 Merhaba `forward-request` İlkesi iletir hello gelen isteği toohello arka uç hizmeti hello istekte belirtilen [bağlamı](api-management-policy-expressions.md#ContextVariables). Merhaba arka uç hizmeti URL'si hello API belirtilen [ayarları](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) ve hello kullanılarak değiştirilebilir [ayarlamak arka uç hizmetini](api-management-transformation-policies.md) ilkesi.  
  
> [!NOTE]
>  Bu ilke sonuçlarını hello giden bölümünde toohello arka uç hizmeti ve hello ilkeleri iletilen değil hello isteğindeki değerlendirilir hemen hello başarılı hello hello ilkelerinde tamamlanmasından sonra kaldırma gelen bölümü.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a>Örnekler  
  
#### <a name="example"></a>Örnek  
 Merhaba aşağıdaki API düzeyi ilkesi tüm istekleri toohello arka uç hizmeti 60 saniye cinsinden bir zaman aşımı aralığı ile iletir.  
  
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
  
#### <a name="example"></a>Örnek  
 Bu işlem düzeyi ilkeyi hello kullanan `base` öğesi tooinherit hello arka uç hello üst API düzeyi kapsam ilkesinden.  
  
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
  
#### <a name="example"></a>Örnek  
 Bu işlem düzeyi ilkesi açıkça tüm istekleri toohello arka uç hizmeti ile bir zaman aşımı süresi 120 iletir ve hello üst API düzeyi arka uç İlkesi devralmaz.  
  
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
  
#### <a name="example"></a>Örnek  
 Bu işlem düzeyi ilkesi isteklerini iletmek değil toohello arka uç hizmeti.  
  
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
  
### <a name="elements"></a>Öğeleri  
  
|Öğesi|Açıklama|Gerekli|  
|-------------|-----------------|--------------|  
|İletme isteği|Kök öğesi.|Evet|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Öznitelik|Açıklama|Gerekli|Varsayılan|  
|---------------|-----------------|--------------|-------------|  
|zaman aşımı = "tamsayı"|Merhaba çağrısı toohello arka uç hizmeti önceki saniye cinsinden zaman aşımı aralığı Hello başarısız olur.|Hayır|Hiçbir zaman aşımı|  
|yeniden yönlendirmeleri izleyin = "true &#124; false"|Yeniden yönlendirmeleri hello arka uç hizmetinden hello gateway tarafından izlenen veya toohello çağıran döndürülen olup olmadığını belirtir.|Hayır|False|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** arka uç  
  
-   **İlke kapsamları:** tüm kapsamlar  
  
##  <a name="LimitConcurrency"></a>Sınır eşzamanlılık  
 Merhaba `limit-concurrency` ilke tarafından belirtilen istek sayısının belirli bir zamanda hello fazlasını yürütülmesini kapalı ilkeleri engeller. Merhaba Eşiği aşan bağlı Hello en büyük sıra uzunluğu elde kadar yeni istekler tooa sıra eklenir. Sıra Tükenme yeni istekleri hemen başarısız olur.
  
###  <a name="LimitConcurrencyStatement"></a>İlke bildirimi  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a>Örnekler  
  
####  <a name="ChooseExample"></a>Örnek  
 Merhaba aşağıdaki örnekte nasıl toolimit istek sayısı bir bağlamının hello değere göre tooa arka uç iletilen gösterir.
 
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

### <a name="elements"></a>Öğeleri  
  
|Öğesi|Açıklama|Gerekli|  
|-------------|-----------------|--------------|    
|sınır eşzamanlılık|Kök öğesi.|Evet|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Öznitelik|Açıklama|Gerekli|Varsayılan|  
|---------------|-----------------|--------------|--------------|  
|anahtar|Bir dize. İzin verilen ifade. Merhaba eşzamanlılık kapsamını belirtir. Birden çok ilke tarafından paylaşılabilir.|Evet|Yok|  
|en yüksek sayısı|Bir tam sayı. En fazla bir tooenter hello ilkesi izin verilen istek sayısını belirtir.|Evet|Yok|  
|Zaman aşımı|Bir tam sayı. İzin verilen ifade. Merhaba bir istek tooenter bir kapsam ile başarısız olmadan önce beklemesi gereken saniye sayısını belirtir "403 çok sayıda istek"|Hayır|Infinity|  
|en büyük sıra uzunluğu|Bir tam sayı. İzin verilen ifade. Merhaba en büyük sıra uzunluğunu belirtir. Gelen istekleri tooenter çalışırken bu ilke ile sona erdirilecek "403 çok sayıda istek" hemen zaman hello sırası tükendi.|Hayır|Infinity|  
  
###  <a name="ChooseUsage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen, giden arka uç, hata  
  
-   **İlke kapsamları:** tüm kapsamlar  

##  <a name="log-to-eventhub"></a>Günlük tooEvent Hub  
 Merhaba `log-to-eventhub` hello iletilerinde belirtilen biçim tooan Event Hub'ın Günlükçü varlık tarafından tanımlanan ilke gönderir. Adından da anlaşılacağı gibi hello İlkesi çevrimiçi veya çevrimdışı analiz için seçilen istek veya yanıt bağlam bilgilerini kaydetmek için kullanılır.  
  
> [!NOTE]
>  Bir olay hub'ı ve olayları günlüğe kaydetmeyi yapılandırma hakkında adım adım yönergeler için bkz: [nasıl toolog API Management olayları Azure Event Hubs ile](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<log-to-eventhub logger-id="id of hello logger entity" partition-id="index of hello partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string toobe logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a>Örnek  
 Herhangi bir dize, olay hub ' oturum hello değeri toobe olarak kullanılabilir. Bu örnekte hello tarih ve saat dağıtım hizmet adı, istek kimliği, IP adresi ve tüm gelen çağrıları için işlem adı oturum toohello event hub'ı Günlükçü hello ile kayıtlı olan `contoso-logger` kimliği.  
  
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
  
### <a name="elements"></a>Öğeleri  
  
|Öğesi|Açıklama|Gerekli|  
|-------------|-----------------|--------------|  
|Günlük eventhub|Kök öğesi. Merhaba bu öğenin hello dize toolog tooyour olay hub'ı değerdir.|Evet|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Öznitelik|Açıklama|Gerekli|  
|---------------|-----------------|--------------|  
|Günlükçü kimliği|Merhaba Hello kimliğini Günlükçü API Management hizmetiniz ile kayıtlı.|Evet|  
|bölüm kimliği|İletilerin gönderileceği hello bölümünün başlangıç dizinini belirtir.|İsteğe bağlı. Bu öznitelik, kullanılamaz. `partition-key` kullanılır.|  
|Bölüm anahtarı|İleti gönderildiğinde bölüm ataması için kullanılan başlangıç değerini belirtir.|İsteğe bağlı. Bu öznitelik, kullanılamaz. `partition-id` kullanılır.|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen, giden arka uç, hata  
  
-   **İlke kapsamları:** tüm kapsamlar  

##  <a name="mock-response"></a>Sahte yanıt  
Merhaba `mock-response`, hello adından da anlaşılacağı, olan kullanılan toomock API'ler ve işlemler. Normal ardışık düzen yürütmesi durdurur ve mocked yanıt toohello çağıran döndürür. Hello İlkesi her zaman en yüksek doğruluk tooreturn yanıtların çalışır. Bu yanıt içerik örnekler, kullanılabilir olduğunda tercih eder. Bu örnek yanıtları şemalarına dönüştürmeyi, şemaları sağlanır ve örnekler olmadıkları zaman oluşturur. Örnek ya da şemaları bulunursa, içerik ile yanıtları döndürülür.
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a>Örnekler  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, hello content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, hello content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a>Öğeleri  
  
|Öğesi|Açıklama|Gerekli|  
|-------------|-----------------|--------------|  
|mock yanıt|Kök öğesi.|Evet|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Öznitelik|Açıklama|Gerekli|Varsayılan|  
|---------------|-----------------|--------------|--------------|  
|Durum kodu|Yanıt durum kodu belirtir ve kullanılan tooselect karşılık gelen örnek veya şema.|Hayır|200|  
|içerik türü|Belirtir `Content-Type` yanıt üstbilgi değeri ve kullanılan tooselect karşılık gelen örnek veya şema.|Hayır|None|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen, giden, hata  
  
-   **İlke kapsamları:** tüm kapsamlar

##  <a name="Retry"></a>Yeniden deneyin  
 Hello `retry` İlkesi kendi alt ilkeleri bir kez çalıştırır ve bunların yürütme hello yeniden deneme kadar yeniden deneme `condition` olur `false` ya da yeniden deneme `count` tükendi olduğu.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
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
  
### <a name="example"></a>Örnek  
 Hello örnek istek forewarding aşağıdaki üstel yeniden deneme algoritması kullanılarak kez tooten yukarı yapılmaya çalışıldı. Bu yana `first-fast-retry` toofalse, ayarlanan tüm denemeleri konu toohello exponsntial yeniden deneme algoritması olan.  
  
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
  
### <a name="elements"></a>Öğeleri  
  
|Öğesi|Açıklama|Gerekli|  
|-------------|-----------------|--------------|  
|Yeniden deneyin|Kök öğesi. Diğer ilkeleri ve alt öğeleri içerebilir.|Evet|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Öznitelik|Açıklama|Gerekli|Varsayılan|  
|---------------|-----------------|--------------|-------------|  
|Koşul|Boole bir hazır değer veya [ifade](api-management-policy-expressions.md) yeniden deneme durmuş olup belirtme (`false`) veya devam (`true`).|Evet|Yok|  
|Sayısı|En fazla yeniden deneme tooattempt Hello yineleneceğini belirten pozitif bir sayı.|Evet|Yok|  
|interval|Merhaba bekleme hello yeniden deneme aralığını belirterek saniye cinsinden pozitif bir sayı.|Evet|Yok|  
|en fazla aralığı|Merhaba en fazla bekleme hello yeniden deneme aralığını belirterek saniye cinsinden pozitif bir sayı. Kullanılan tooimplement üstel yeniden deneme algoritması olur.|Hayır|Yok|  
|Delta|Merhaba bekleme aralığı artırma belirtme saniye cinsinden pozitif bir sayı. Kullanılan tooimplement hello doğrusal ve üstel yeniden deneme algoritmaları olur.|Hayır|Yok|  
|ilk hızlı yeniden|Varsa çok ayarlamak `true` , hello ilk yeniden deneme girişimi hemen gerçekleştirilir.|Hayır|`false`|  
  
> [!NOTE]
>  Ne zaman yalnızca hello `interval` belirtilirse, **sabit** aralığı yeniden denemeler gerçekleştirilir.  
>  Ne zaman yalnızca hello `interval` ve `delta` belirtilir, bir **doğrusal** aralığı yeniden deneme algoritması kullanılır, denemeler arasındaki bekleme süresini hesaplanan according hello olduğu formülü - aşağıdaki `interval + (count - 1)*delta`.  
>  Ne zaman hello `interval`, `max-interval` ve `delta` belirtilir, **üstel** aralığı yeniden deneme algoritması uygulandığında, burada hello bekleme süresi hello denemeler arasındaki Başlangıçdeğerindenkatlanarakartıyor`interval`toohello değeri `max-interval` toohello aşağıdaki göre forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) . Alt İlkesi kullanım kısıtlamaları Bu ilke tarafından devralınır unutmayın.  
  
-   **İlke bölümleri:** gelen, giden arka uç, hata  
  
-   **İlke kapsamları:** tüm kapsamlar  
  
##  <a name="ReturnResponse"></a>Yanıt döndürür  
 Merhaba `return-response` İlkesi ardışık düzen yürütmesi durdurur ve bir varsayılan veya özel yanıt toohello çağıran döndürür. Varsayılan yanıt `200 OK` hiçbir gövde ile. Özel yanıtı bağlam değişkeni veya ilke deyimleri ile belirtilebilir. Her ikisi de sağlandığında, hello bağlamının içinde yer alan hello yanıt toohello çağıran döndürülen önce hello İlkesi deyimleri tarafından değiştirilir.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a>Örnek  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a>Öğeleri  
  
|Öğesi|Açıklama|Gerekli|  
|-------------|-----------------|--------------|  
|return yanıt|Kök öğesi.|Evet|  
|set üstbilgisi|A [set üstbilgisi](api-management-transformation-policies.md#SetHTTPheader) ilke bildirimi.|Hayır|  
|set-gövdesi|A [kümesi gövde](api-management-transformation-policies.md#SetBody) ilke bildirimi.|Hayır|  
|durumunu ayarla|A [durumunu ayarla](api-management-advanced-policies.md#SetStatus) ilke bildirimi.|Hayır|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Öznitelik|Açıklama|Gerekli|  
|---------------|-----------------|--------------|  
|yanıt değişken adı|Merhaba hello bağlamının adı, örneğin, Yukarı Akış başvurulan [gönderme isteği](api-management-advanced-policies.md#SendRequest) ilke ve içeren bir `Response` nesnesi|İsteğe bağlı.|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen, giden arka uç, hata  
  
-   **İlke kapsamları:** tüm kapsamlar  
  
##  <a name="SendOneWayRequest"></a>Tek yönlü İsteği Gönder  
 Merhaba `send-one-way-request` ilke toohello belirtilen URL için bir yanıt beklemeden sağlanan hello isteği gönderir.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a>Örnek  
 Bu örnek ilke hello kullanmanın bir örneği gösterir `send-one-way-request` İlkesi toosend bir ileti tooa Slack sohbet hello HTTP yanıt kodunu büyük veya ona eşit too500 ise odası. Bu örnek hakkında daha fazla bilgi için bkz: [dış Hizmetleri'nden hello Azure API Management hizmeti kullanarak](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).  
  
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
  
### <a name="elements"></a>Öğeleri  
  
|Öğesi|Açıklama|Gerekli|  
|-------------|-----------------|--------------|  
|bir şekilde İsteği Gönder|Kök öğesi.|Evet|  
|URL|Merhaba isteği Hello URL'si.|Hiçbir IF modu kopyalama; = Aksi takdirde Evet.|  
|Yöntemi|Merhaba hello isteği için HTTP yöntemi.|Hiçbir IF modu kopyalama; = Aksi takdirde Evet.|  
|üst bilgi|İstek üstbilgisi. Birden çok üstbilgi öğeleri için birden çok istek üstbilgileri kullanın.|Hayır|  
|Gövde|Merhaba istek gövdesi.|Hayır|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Öznitelik|Açıklama|Gerekli|Varsayılan|  
|---------------|-----------------|--------------|-------------|  
|modu = "dize"|Yeni bir istek veya bir kopyasını hello geçerli istek olup olmadığını belirler. Giden modunda modu = kopyalama hello istek gövdesi başlatamadı.|Hayır|Yeni|  
|ad|Merhaba hello üstbilgi toobe kümesinin adını belirtir.|Evet|Yok|  
|Mevcut eylem|Merhaba üstbilgi zaten belirtildiğinde hangi eylemini tootake belirtir. Bu öznitelik değerlerini aşağıdaki hello birine sahip olmalıdır.<br /><br /> -değiştirir hello hello varolan üstbilgisinin değerini geçersiz kıl -.<br />-skip - hello varolan üstbilgi değeri değiştirmez.<br />-Ekle - hello değeri toohello varolan üstbilgi değeri ekler.<br />-delete - hello üstbilgisini hello isteğinden kaldırır.<br /><br /> Ayarlandığında çok`override` birden çok girişi kaydetme; hello ile aynı sonuçları (birden çok kez listelenir) kümesi according tooall girdisi olan hello üstbilgisinde adı yalnızca listelenen değerler hello sonucunda ayarlanır.|Hayır|geçersiz kılma|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen, giden arka uç, hata  
  
-   **İlke kapsamları:** tüm kapsamlar  
  
##  <a name="SendRequest"></a>İsteği Gönder  
 Merhaba `send-request` ilke toohello belirtilen zaman aşımı değerini hello ayarlamak daha artık bekleyen URL, sağlanan hello isteği gönderir.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a>Örnek  
 Bu örnek, başvuru belirteci yetkilendirme sunucusu ile tek yönlü tooverify gösterir. Bu örnek hakkında daha fazla bilgi için bkz: [dış Hizmetleri'nden hello Azure API Management hizmeti kullanarak](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).  
  
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
  
### <a name="elements"></a>Öğeleri  
  
|Öğesi|Açıklama|Gerekli|  
|-------------|-----------------|--------------|  
|Gönderme isteği|Kök öğesi.|Evet|  
|URL|Merhaba isteği Hello URL'si.|Hiçbir IF modu kopyalama; = Aksi takdirde Evet.|  
|Yöntemi|Merhaba hello isteği için HTTP yöntemi.|Hiçbir IF modu kopyalama; = Aksi takdirde Evet.|  
|üst bilgi|İstek üstbilgisi. Birden çok üstbilgi öğeleri için birden çok istek üstbilgileri kullanın.|Hayır|  
|Gövde|Merhaba istek gövdesi.|Hayır|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Öznitelik|Açıklama|Gerekli|Varsayılan|  
|---------------|-----------------|--------------|-------------|  
|modu = "dize"|Yeni bir istek veya bir kopyasını hello geçerli istek olup olmadığını belirler. Giden modunda modu = kopyalama hello istek gövdesi başlatamadı.|Hayır|Yeni|  
|yanıt değişkeni adı = "dize"|Yoksa, `context.Response` kullanılır.|Hayır|Yok|  
|zaman aşımı = "tamsayı"|Merhaba zaman aşımı aralığı saniye hello çağrıdan önce toohello URL başarısız olur.|Hayır|60|  
|Hatayı Yoksay|Doğru ve hello hatayla sonuçlanır isterse:<br /><br /> -Eğer bir null değer içerecek yanıt değişkeni adı belirtildi.<br />-Yanıt değişkeni adı belirtilmedi Eğer bağlamı. İstek güncelleştirilmez.|Hayır|False|  
|ad|Merhaba hello üstbilgi toobe kümesinin adını belirtir.|Evet|Yok|  
|Mevcut eylem|Merhaba üstbilgi zaten belirtildiğinde hangi eylemini tootake belirtir. Bu öznitelik değerlerini aşağıdaki hello birine sahip olmalıdır.<br /><br /> -değiştirir hello hello varolan üstbilgisinin değerini geçersiz kıl -.<br />-skip - hello varolan üstbilgi değeri değiştirmez.<br />-Ekle - hello değeri toohello varolan üstbilgi değeri ekler.<br />-delete - hello üstbilgisini hello isteğinden kaldırır.<br /><br /> Ayarlandığında çok`override` birden çok girişi kaydetme; hello ile aynı sonuçları (birden çok kez listelenir) kümesi according tooall girdisi olan hello üstbilgisinde adı yalnızca listelenen değerler hello sonucunda ayarlanır.|Hayır|geçersiz kılma|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen, giden arka uç, hata  
  
-   **İlke kapsamları:** tüm kapsamlar  
  
##  <a name="SetHttpProxy"></a>Set HTTP proxy  
 Merhaba `proxy` İlkesi tooroute iletilen istekleri toobackends bir HTTP proxy üzerinden sağlar. Yalnızca HTTP (HTTPS değil) hello ağ geçidi ve hello proxy arasında desteklenir. Temel ve yalnızca NTLM kimlik doğrulaması.
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a>Örnek  
Not hello [özellikleri](api-management-howto-properties.md) hello İlkesi belgede hassas bilgileri depolamak hello kullanıcı adı ve parola tooavoid değerleri olarak.  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a>Öğeleri  
  
|Öğesi|Açıklama|Gerekli|  
|-------------|-----------------|--------------|  
|Proxy|Kök öğesi|Evet|  

### <a name="attributes"></a>Öznitelikler  
  
|Öznitelik|Açıklama|Gerekli|Varsayılan|  
|---------------|-----------------|--------------|-------------|  
|URL = "dize"|Proxy URL'si http://host:port hello biçiminde.|Evet|Yok|  
|Kullanıcı adı = "dize"|Kullanıcı adı toobe hello proxy kimlik doğrulaması için kullanılır.|Hayır|Yok|  
|parola = "dize"|Parola toobe hello proxy kimlik doğrulaması için kullanılır.|Hayır|Yok|  

### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen  
  
-   **İlke kapsamları:** tüm kapsamlar  

##  <a name="SetRequestMethod"></a>Set isteği yöntemi  
 Merhaba `set-method` ilke isteği için toochange hello HTTP istek yöntemi sağlar.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a>Örnek  
 Merhaba kullanan bu örnek ilke `set-method` ilke hello HTTP yanıt kodunu büyükse bir ileti tooa Slack sohbet odası gönderirken ya da eşit too500 örneği gösterir. Bu örnek hakkında daha fazla bilgi için bkz: [dış Hizmetleri'nden hello Azure API Management hizmeti kullanarak](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).  
  
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
  
### <a name="elements"></a>Öğeleri  
  
|Öğesi|Açıklama|Gerekli|  
|-------------|-----------------|--------------|  
|Set yöntemi|Kök öğesi. Merhaba öğesinin Hello değeri hello HTTP yöntemini belirtir.|Evet|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen, hata  
  
-   **İlke kapsamları:** tüm kapsamlar  
  
##  <a name="SetStatus"></a>Set durum kodu  
 Merhaba `set-status` ilke kümeleri hello HTTP durum kodu toohello belirtilen değeri.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a>Örnek  
 Bu örnekte gösterilir nasıl tooreturn hello yetkilendirme belirteci geçersiz ise 401 yanıt. Daha fazla bilgi için bkz: [hello Azure API Management hizmeti dış Hizmetleri'nden kullanma](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)  
  
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
  
### <a name="elements"></a>Öğeleri  
  
|Öğesi|Açıklama|Gerekli|  
|-------------|-----------------|--------------|  
|durumunu ayarla|Kök öğesi.|Evet|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Öznitelik|Açıklama|Gerekli|Varsayılan|  
|---------------|-----------------|--------------|-------------|  
|kod = "tamsayı"|Merhaba HTTP durum kodu tooreturn.|Evet|Yok|  
|nedeni = "dize"|Merhaba durum kodu döndürmek için hello neden açıklaması.|Evet|Yok|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** giden, arka uç, hata  
  
-   **İlke kapsamları:** tüm kapsamlar  

##  <a name="set-variable"></a>Değişken Ayarla  
 Hello `set-variable` İlkesi bildirir bir [bağlamı](api-management-policy-expressions.md#ContextVariables) değişkeni aracılığıyla belirtilen bir değeri atar bir [ifade](api-management-policy-expressions.md) veya bir değişmez dize değeri. Merhaba ifadesi, dönüştürülmesi bir hazır değer içeriyorsa hello değerin tooa dize ve hello türü olacaktır `System.String`.  
  
###  <a name="set-variablePolicyStatement"></a>İlke bildirimi  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <a name="set-variableExample"></a>Örnek  
 Merhaba aşağıdaki örnekte gösterilmiştir hello kümesi değişken ilkesinde gelen bölümü. Bu değişken ilkesini ayarlama oluşturur bir `isMobile` Boolean [bağlamı](api-management-policy-expressions.md#ContextVariables) tootrue hello ayarlanır değişkeni `User-Agent` istek üstbilgisi hello metni içerir `iPad` veya `iPhone`.  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a>Öğeleri  
  
|Öğesi|Açıklama|Gerekli|  
|-------------|-----------------|--------------|  
|değişken Ayarla|Kök öğesi.|Evet|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Öznitelik|Açıklama|Gerekli|  
|---------------|-----------------|--------------|  
|ad|Merhaba değişkeninin Hello adı.|Evet|  
|değer|Merhaba değişkenin Hello değeri. Bu bir deyim veya bir hazır değer olabilir.|Evet|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen, giden arka uç, hata  
  
-   **İlke kapsamları:** tüm kapsamlar  
  
###  <a name="set-variableAllowedTypes"></a>İzin verilen türleri  
 Hello kullanılan ifadeleri `set-variable` İlkesi şu temel türlerini hello birini döndürmesi gerekir.  
  
-   System.Boolean  
  
-   System.SByte  
  
-   System.Byte  
  
-   System.UInt16  
  
-   System.UInt32  
  
-   System.UInt64  
  
-   System.Int16  
  
-   System.Int32  
  
-   System.Int64  
  
-   System.Decimal  
  
-   System.Single  
  
-   System.Double  
  
-   System.Guid  
  
-   System.String  
  
-   System.Char  
  
-   System.DateTime  
  
-   System.TimeSpan  
  
-   System.Byte?  
  
-   System.UInt16?  
  
-   System.UInt32?  
  
-   System.UInt64?  
  
-   System.Int16?  
  
-   System.Int32?  
  
-   System.Int64?  
  
-   System.Decimal?  
  
-   System.Single?  
  
-   System.Double?  
  
-   System.Guid?  
  
-   System.String?  
  
-   System.Char?  
  
-   System.DateTime?  

##  <a name="Trace"></a>İzleme  
 Merhaba `trace` İlkesi hello bir dize ekler [API denetçisi](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) çıktı. Hello ilkesi yalnızca, izleme, yani tetiklenir yürütecek `Ocp-Apim-Trace` istek üstbilgisi varsa ve çok`true` ve `Ocp-Apim-Subscription-Key` istek üstbilgisi bulunduğundan ve hello yönetici hesabıyla ilişkilendirilmiş geçerli bir anahtar tutar.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a>Öğeleri  
  
|Öğesi|Açıklama|Gerekli|  
|-------------|-----------------|--------------|  
|İzleme|Kök öğesi.|Evet|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Öznitelik|Açıklama|Gerekli|Varsayılan|  
|---------------|-----------------|--------------|-------------|  
|Kaynak|Dize değişmez değer anlamlı toohello izleme Görüntüleyicisi'ni ve belirten hello kaynağı hello iletisi.|Evet|Yok|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .  
  
-   **İlke bölümleri:** gelen, giden arka uç, hata  
  
-   **İlke kapsamları:** tüm kapsamlar  
  
##  <a name="Wait"></a>Bekleme  
 Merhaba `wait` ilke hemen alt ilkelerine paralel olarak yürütür ve tamamlanmadan önce tüm ya da kendi hemen alt ilkeleri toocomplete biri için bekler. Merhaba bekleme ilke hemen alt ilkelerine olabilir [gönderme isteği](api-management-advanced-policies.md#SendRequest), [değeri önbellekten alma](api-management-caching-policies.md#GetFromCacheByKey), ve [kontrol akışı](api-management-advanced-policies.md#choose) ilkeleri.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a>Örnek  
 Aşağıdaki örneğine hello vardır iki `choose` ilkeleri hello hemen alt ilkelerini olarak `wait` ilkesi. Bunların her biri `choose` ilkeleri paralel olarak yürütür. Her `choose` İlkesi, bir önbelleğe alınan değer tooretrieve çalışır. Önbellek isabetsizliği varsa, arka uç hizmeti tooprovide hello değer adı verilir. Bu örnek hello içinde `wait` İlkesi tamamlamaz hemen alt ilkeler tamamlanana kadar çünkü hello `for` özniteliği olarak ayarlanmış çok`all`.   Bu örnek hello bağlam değişkenlerine (`execute-branch-one`, `value-one`, `execute-branch-two`, ve `value-two`) Bu örnek ilke hello kapsamı dışında bildirilir.  
  
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
  
### <a name="elements"></a>Öğeleri  
  
|Öğesi|Açıklama|Gerekli|  
|-------------|-----------------|--------------|  
|bekleme|Kök öğesi. Yalnızca alt öğeleri içerebilir `send-request`, `cache-lookup-value`, ve `choose` ilkeleri.|Evet|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Öznitelik|Açıklama|Gerekli|Varsayılan|  
|---------------|-----------------|--------------|-------------|  
|için|Hello olup olmadığını belirleyen `wait` İlkesi bekler tamamlandı tüm hemen alt ilkeleri toobe için veya tek bir. İzin verilen değerler:<br /><br /> -   `all`-Tüm hemen alt ilkeleri toocomplete için bekleyin<br />-any - tüm hemen alt ilke toocomplete için bekleyin. Merhaba ilk hemen alt ilke tamamlandıktan sonra hello `wait` ilkeyi tamamladıktan ve diğer hemen alt ilkeleri yürütülmesi biter.|Hayır|Tüm|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen, giden arka uç  
  
-   **İlke kapsamları:**tüm kapsamlar  
  
## <a name="next-steps"></a>Sonraki adımlar
İlkeleriyle çalışma daha fazla bilgi için bkz:
-   [API Management ilkeleri](api-management-howto-policies.md) 
-   [İlke ifadeleri](api-management-policy-expressions.md)
