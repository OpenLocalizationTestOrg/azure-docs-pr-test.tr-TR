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
# <a name="api-management-transformation-policies"></a>API Management dönüştürme ilkelerini
Bu konuda API Management ilkelere hello için bir başvuru sağlar. Ekleme ve ilkeleri yapılandırma hakkında daha fazla bilgi için bkz: [API Management ilkeleri](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="TransformationPolicies"></a>Dönüştürme ilkelerini  
  
-   [JSON tooXML Dönüştür](api-management-transformation-policies.md#ConvertJSONtoXML) - dönüştürür istek veya yanıt gövdesi JSON tooXML.  
  
-   [XML tooJSON Dönüştür](api-management-transformation-policies.md#ConvertXMLtoJSON) - dönüştürür istek veya yanıt gövdesi XML tooJSON.  
  
-   [Bulma ve değiştirme dizesi gövdesi içinde](api-management-transformation-policies.md#Findandreplacestringinbody) - bir istek veya yanıt alt dizeyi bulur ve farklı bir dizeyle değiştirir.  
  
-   [İçeriği URL'leri maske](api-management-transformation-policies.md#MaskURLSContent) -(maskeleri)'yeniden yazar bağlantılar hello yanıt gövdesi böylece hello ağ geçidi aracılığıyla toohello eşdeğer bağlantı noktası.  
  
-   [Arka uç hizmetini ayarlamak](api-management-transformation-policies.md#SetBackendService) -değişiklikleri hello arka uç hizmetine gelen bir istek için.  
  
-   [Gövde ayarlamak](api-management-transformation-policies.md#SetBody) -hello ileti gövdesi gelen ve giden istekleri için ayarlar.  
  
-   [HTTP üstbilgisi kümesi](api-management-transformation-policies.md#SetHTTPheader) - değer tooan varolan yanıt ve/veya istek üstbilgisi atar veya yeni bir yanıt ve/veya istek üstbilgisi ekler.  
  
-   [Sorgu dizesi parametresi kümesi](api-management-transformation-policies.md#SetQueryStringParameter) - ekler, değiştirir değerini veya istek sorgu dizesi parametresi siler.  
  
-   [URL yeniden yazma](api-management-transformation-policies.md#RewriteURL) -hello web hizmeti tarafından beklenen genel form toohello formundan bir istek URL'sini dönüştürür.  
  
-   [XSLT kullanarak XML dönüştürme](api-management-transformation-policies.md#XSLTransform) -bir XSL Dönüştürme tooXML hello istek veya yanıt gövdesi içinde geçerlidir.  
  
##  <a name="ConvertJSONtoXML"></a>JSON tooXML Dönüştür  
 Merhaba `json-to-xml` ilkeyi JSON tooXML bir istek veya yanıt gövdesi dönüştürür.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a>Örnek  
  
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
  
### <a name="elements"></a>Öğeleri  
  
|Ad|Açıklama|Gerekli|  
|----------|-----------------|--------------|  
|JSON xml|Kök öğesi.|Evet|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Ad|Açıklama|Gerekli|Varsayılan|  
|----------|-----------------|--------------|-------------|  
|Uygula|Merhaba öznitelik değerleri aşağıdaki hello tooone ayarlamanız gerekir.<br /><br /> -her zaman - her zaman dönüştürme uygulanır.<br />Yalnızca yanıt Content-Type üstbilgisi JSON varlığını gösteriyorsa - içerik türü json - dönüştürülemiyor.|Evet|Yok|  
|göz önünde bulundurun kabul-üstbilgisi|Merhaba öznitelik değerleri aşağıdaki hello tooone ayarlamanız gerekir.<br /><br /> JSON istek Accept üstbilgisi isteniyorsa - true - dönüştürme uygulanır.<br />-false - her zaman dönüştürme uygulayın.|Hayır|TRUE|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen, giden, hata  
  
-   **İlke kapsamları:** genel, ürün, API işlemi  
  
##  <a name="ConvertXMLtoJSON"></a>XML tooJSON Dönüştür  
 Merhaba `xml-to-json` ilkeyi XML tooJSON bir istek veya yanıt gövdesi dönüştürür. Bu ilke API'leri yalnızca XML arka uç web hizmetlerini temel alarak kullanılan toomodernize olabilir.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a>Örnek  
  
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
  
### <a name="elements"></a>Öğeleri  
  
|Ad|Açıklama|Gerekli|  
|----------|-----------------|--------------|  
|XML json|Kök öğesi.|Evet|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Ad|Açıklama|Gerekli|Varsayılan|  
|----------|-----------------|--------------|-------------|  
|türü|Merhaba öznitelik değerleri aşağıdaki hello tooone ayarlamanız gerekir.<br /><br /> -javascript kolay - hello dönüştürülen JSON bir form kolay tooJavaScript geliştiriciler sahiptir.<br />-doğrudan - hello dönüştürülen JSON hello özgün XML belge yapısını yansıtır.|Evet|Yok|  
|Uygula|Merhaba öznitelik değerleri aşağıdaki hello tooone ayarlamanız gerekir.<br /><br /> -her zaman - her zaman dönüştürün.<br />Yalnızca yanıt Content-Type üstbilgisi XML varlığını gösteriyorsa - içerik türü xml - dönüştürülemiyor.|Evet|Yok|  
|göz önünde bulundurun kabul-üstbilgisi|Merhaba öznitelik değerleri aşağıdaki hello tooone ayarlamanız gerekir.<br /><br /> XML isteği Accept üstbilgisi isteniyorsa - true - dönüştürme uygulanır.<br />-false - her zaman dönüştürme uygulayın.|Hayır|TRUE|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen, giden, hata  
  
-   **İlke kapsamları:** genel, ürün, API işlemi  
  
##  <a name="Findandreplacestringinbody"></a>Bulma ve gövde dizesinde değiştirme  
 Merhaba `find-and-replace` ilke isteği veya yanıtı alt dizeyi bulur ve farklı bir dizeyle değiştirir.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<find-and-replace from="what tooreplace" to="replacement" />  
```  
  
### <a name="example"></a>Örnek  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a>Öğeleri  
  
|Ad|Açıklama|Gerekli|  
|----------|-----------------|--------------|  
|Bul ve Değiştir|Kök öğesi.|Evet|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Ad|Açıklama|Gerekli|Varsayılan|  
|----------|-----------------|--------------|-------------|  
|Kaynak|Merhaba dize toosearch için.|Evet|Yok|  
|-|Merhaba değiştirme dizesi. Sıfır uzunluk değiştirme dizesi tooremove hello arama dizesi belirtin.|Evet|Yok|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen, giden arka uç, hata  
  
-   **İlke kapsamları:** genel, ürün, API işlemi  
  
##  <a name="MaskURLSContent"></a>İçerik maskesi URL'leri  
 Merhaba `redirect-content-urls` İlkesi hello ağ geçidi aracılığıyla toohello eşdeğer bağlantı noktası böylece hello yanıt gövdesi (maskeleri) bağlantıları yeniden yazar. Merhaba giden bölüm toore yazma yanıt gövdesi bağlantılar toomake bunları noktası toohello ağ geçidi kullanın. Merhaba kullanımda gelen ters efekt bölümü.  
  
> [!NOTE]
>  Bu ilke tüm üstbilgi değerleri gibi değiştirmez `Location` üstbilgileri. toochange üstbilgi değerleri kullanmak hello [set üstbilgisi](api-management-transformation-policies.md#SetHTTPheader) ilkesi.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a>Örnek  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a>Öğeleri  
  
|Ad|Açıklama|Gerekli|  
|----------|-----------------|--------------|  
|Yönlendirme içerik URL'leri|Kök öğesi.|Evet|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen, giden  
  
-   **İlke kapsamları:** genel, ürün, API işlemi  
  
##  <a name="SetBackendService"></a>Arka uç hizmet belirleme  
 Kullanım hello `set-backend-service` İlkesi tooredirect gelen bir istek tooa farklı arka uç bir hello API ayarları bu işlem için belirtilen hello daha. Bu ilke hello arka uç hizmeti temel URL'sini hello gelen isteği toohello bir hello İlkesi'nde belirtilen değiştirir.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<set-backend-service base-url="base URL of hello backend service" />  
```  
  
### <a name="example"></a>Örnek  
  
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
Bu örnek hello arka uç hizmeti ilkesini ayarlama hello sorgu dizesi tooa farklı arka uç hizmeti hello bir belirtilen hello API'den geçirilen hello sürüm değere göre isteklerini yönlendirir.
  
Başlangıçta hello arka uç hizmeti temel URL'si hello API ayarlarından türetilir. Böylece istek URL'si hello `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` hale `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` burada `http://contoso.com/api/10.4/` hello API ayarlarında belirtilen hello arka uç hizmeti URL.  
  
Ne zaman hello [< seçin\> ](api-management-advanced-policies.md#choose) ilke bildirimi uygulanır hello arka uç hizmeti temel URL'si değişebilir yeniden ya da çok`http://contoso.com/api/8.2` veya `http://contoso.com/api/9.1`hello hello sürüm istek sorgu parametresinin değerini bağlı olarak. Örneğin, hello değer ise `"2013-15"` hello son istek URL'si hale `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.  
  
Daha fazla dönüştürme hello isteği olup olmadığını istenen, diğer [dönüştürme ilkelerini](api-management-transformation-policies.md#TransformationPolicies) kullanılabilir. Merhaba istek bırakılıyor göre parametre yönlendirilen tooa sürüm belirli arka uç, hello Örneğin, tooremove hello sürüm sorgu [ayarlamak sorgu dizesi parametresi](api-management-transformation-policies.md#SetQueryStringParameter) İlkesi kullanılan tooremove hello şimdi yedek sürüm özniteliği olamaz.  
  
### <a name="example"></a>Örnek  
  
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
Bu örnek hello İlkesi yollar hello isteği tooa hizmet doku arka uç içinde hello UserID sorgu dizesi hello bölüm anahtarı olarak kullanma ve kullanma hello bölümünün birincil çoğaltmasını hello.  

### <a name="elements"></a>Öğeleri  
  
|Ad|Açıklama|Gerekli|  
|----------|-----------------|--------------|  
|arka uç hizmet belirleme|Kök öğesi.|Evet|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Ad|Açıklama|Gerekli|Varsayılan|  
|----------|-----------------|--------------|-------------|  
|Taban URL'si|Yeni arka uç hizmeti temel URL'si.|Hayır|Yok|  
|arka uç kimliği|Merhaba arka uç tooroute tanımlayıcısı.|Hayır|Yok|  
|BT bölüm anahtarı|Yalnızca hello arka uç Service Fabric hizmeti ve 'arka uç-ID' kullanılarak belirtilen olduğunda geçerlidir. Tooresolve hello ad çözümleme hizmeti belirli bir bölümünden kullanılır.|Hayır|Yok|  
|BT çoğaltma türü|Yalnızca hello arka uç Service Fabric hizmeti ve 'arka uç-ID' kullanılarak belirtilen olduğunda geçerlidir. Bir bölümün toohello birincil veya ikincil çoğaltma Hello isteği görünmeliyse denetler. |Hayır|Yok|    
|BT çözümleme durumu|Yalnızca hello arka uç Service Fabric hizmeti olduğunda geçerlidir. Merhaba tooService doku arka uç çağırırsanız koşulu tanımlayan yeni bir çözümleme yinelenen toobe sahiptir.|Hayır|Yok|    
|BT hizmet örneği adı|Yalnızca hello arka uç Service Fabric hizmeti olduğunda geçerlidir. Toochange çalışma zamanında hizmet örnekleri sağlar. |Hayır|Yok|    

### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen, arka uç  
  
-   **İlke kapsamları:** genel, ürün, API işlemi  
  
##  <a name="SetBody"></a>Set gövdesi  
 Kullanım hello `set-body` gelen ve giden istekleri için ilke tooset hello ileti gövdesi. tooaccess hello hello kullanabileceğiniz ileti gövdesi `context.Request.Body` özelliği veya hello `context.Response.Body`hello İlkesi hello olmasına bağlı olarak gelen veya giden bölümü.  
  
> [!IMPORTANT]
>  Siz eriştiğinizde, varsayılan ileti gövdesi kullanarak hello unutmayın `context.Request.Body` veya `context.Response.Body`, gövde kaybolur ve geri hello ifadesinde hello gövde döndürerek ayarlanmalıdır hello özgün ileti. toopreserve hello gövdesi içeriği ayarlamak hello `preserveContent` parametresi çok`true` selamlama iletisine erişirken. Varsa `preserveContent` çok ayarlanır`true` ve hello döndürülen gövde kullanılır farklı gövde hello ifadeyle döndürülür.  
>   
>  Lütfen dikkat edilecek noktalar hello kullanırken aşağıdaki hello Not `set-body` ilkesi.  
>   
>  -   Merhaba kullanıyorsanız `set-body` İlkesi tooreturn tooset gerekmez yeni veya güncelleştirilmiş bir gövde `preserveContent` çok`true` çünkü hello yeni gövdesi içeriği açıkça sağlamış olursunuz.  
> -   Olmadığından yanıt henüz hello gelen ardışık düzeninde bir yanıt Merhaba içeriğine koruma doesn't make Sense.  
> -   Merhaba istek zaten toohello arka uç bu noktada gönderildi çünkü hello giden ardışık düzeninde bir istek Merhaba içeriğine koruma doesn't make Sense.  
> -   Örneğin ileti gövdesi yok olduğunda bu ilkeyi kullandıysanız, gelen bir GET içinde bir özel durum oluşur.  
  
 Merhaba daha fazla bilgi için bkz: `context.Request.Body`, `context.Response.Body`ve hello `IMessage` hello bölümlerde [bağlamının](api-management-policy-expressions.md#ContextVariables) tablo.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a>Örnekler  
  
#### <a name="literal-text-example"></a>Değişmez değer metni örneği  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-string-note-that-we-are-preserving-hello-original-request-body-so-that-we-can-access-it-later-in-hello-pipeline"></a>Örnek, dize olarak Hello gövdesi erişme. Biz bunu daha sonra hello ardışık düzeninde erişebilmesi için biz hello özgün istek gövdesi koruma olduğunu unutmayın.
  
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
  
#### <a name="example-accessing-hello-body-as-a-jobject-note-that-since-we-are-not-reserving-hello-original-request-body-accesing-it-later-in-hello-pipeline-will-result-in-an-exception"></a>Örnek Hello gövdesi bir JObject olarak erişme. Biz hello özgün istek gövdesi, bunu daha sonra hello ardışık düzeninde bir özel durumla sonuçlanır belirtilmemelidir ayırma değil bu yana unutmayın.  
  
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
  
#### <a name="filter-response-based-on-product"></a>Ürüne göre filtre yanıtı  
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

### <a name="using-liquid-templates-with-set-body"></a>Set gövde ile sıvı şablonlarını kullanma 
Merhaba `set-body` İlkesi, yapılandırılmış toouse hello olabilir [sıvı](https://shopify.github.io/liquid/basics/introduction/) şablon dili tootransfom hello gövdesi bir istek veya yanıt. Bu iletinin toocompletely yeniden şekillendirme hello biçimi gerekiyorsa çok etkili olabilir.

> [!IMPORTANT]
> hello kullanılan sıvı uyarlamasını hello `set-body` ilke ', C# modu' yapılandırılır. Bu filtreleme gibi şeyler yaparken özellikle önemlidir. Örnek olarak, bir tarih filtresi kullanarak Pascal hello kullanılmasını gerektiren büyük/küçük harf ve C# tarih biçimlendirme örn:
>
> {{body.foo.startDateTime| Tarih: "yyyyMMddTHH:mm:ddZ"}}

> [!IMPORTANT]
> Hello sıvı şablonu kullanarak sipariş toocorrectly bağlama tooan XML metninde kullanmak bir `set-header` İlkesi tooset Content-Type tooeither uygulama/xml, text/xml (veya tüm ile biten türü + xml); JSON gövdesi için uygulama/json, text/json (veya tüm türü bitiş olmalıdır ile + json).

#### <a name="convert-json-toosoap-using-a-liquid-template"></a>Sıvı bir şablon kullanarak JSON tooSOAP Dönüştür
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

#### <a name="tranform-json-using-a-liquid-template"></a>Dönüşüm sıvı bir şablon kullanarak JSON
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a>Öğeleri  
  
|Ad|Açıklama|Gerekli|  
|----------|-----------------|--------------|  
|set-gövdesi|Kök öğesi. Merhaba gövde metin ya da body döndüren bir ifade içeriyor.|Evet|  

### <a name="properties"></a>Özellikler  
  
|Ad|Açıklama|Gerekli|Varsayılan|  
|----------|-----------------|--------------|-------------|  
|şablon|Gövde ilkesini ayarlama hello kullanılan toochange hello şablon oluşturma modunda çalıştırmak. Şu anda yalnızca desteklenen hello değeri şudur:<br /><br />-Sıvı - hello gövde ilkesini ayarlama hello sıvı şablon altyapısı kullanır |Hayır|Sıvı|  

Hello istek ve yanıt bilgilerine erişmek için hello sıvı şablonu tooa bağlam nesnesi aşağıdaki özelliklere hello ile bağlayabilirsiniz: <br />
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



### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen, giden arka uç  
  
-   **İlke kapsamları:** genel, ürün, API işlemi  
  
##  <a name="SetHTTPheader"></a>HTTP üstbilgisi kümesi  
 Merhaba `set-header` ilke değeri tooan varolan yanıt ve/veya istek üstbilgisi atar veya yeni bir yanıt ve/veya istek üstbilgisi ekler.  
  
 HTTP üstbilgilerin listesi HTTP iletisine ekler. Bir gelen ardışık düzeninde yerleştirildiğinde, bu ilkeyi toohello hedef hizmet geçirilen hello isteği hello HTTP üstbilgilerini ayarlar. Giden ardışık düzeninde yerleştirildiğinde, bu ilkeyi toohello ağ geçidi istemci gönderilen hello yanıt hello HTTP üstbilgilerini ayarlar.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with hello same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a>Örnekler  
  
#### <a name="example"></a>Örnek  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a>Bağlam bilgileri toohello arka uç hizmeti ilet  
 Bu örnek, tooapply İlkesi hello API düzey toosupply bağlam bilgileri toohello arka uç hizmetini nasıl gösterir. Yapılandırma ve bu ilkeyi kullanan bir örnek için bkz: [bulut kapak bölüm 177: daha Vlad Vinogradsky ile yönetim özelliklerini API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) ve too10:30 ileri sarma. 12:10 İşte hello İlkesi görebileceğiniz bir işlem hello Geliştirici Portalı'nda arama demo yoktur.  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward some context information, user id and hello region hello gateway is hosted in, toohello backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 Daha fazla bilgi için bkz: [ilke ifadelerini](api-management-policy-expressions.md) ve [bağlamının](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="elements"></a>Öğeleri  
  
|Ad|Açıklama|Gerekli|  
|----------|-----------------|--------------|  
|set üstbilgisi|Kök öğesi.|Evet|  
|değer|Merhaba üstbilgi toobe kümesi Hello değerini belirtir. Merhaba ile birden çok üst bilgileri için aynı adı ekle ek `value` öğeleri.|Evet|  
  
### <a name="properties"></a>Özellikler  
  
|Ad|Açıklama|Gerekli|Varsayılan|  
|----------|-----------------|--------------|-------------|  
|Mevcut eylem|Merhaba üstbilgi zaten belirtildiğinde hangi eylemini tootake belirtir. Bu öznitelik değerlerini aşağıdaki hello birine sahip olmalıdır.<br /><br /> -değiştirir hello hello varolan üstbilgisinin değerini geçersiz kıl -.<br />-skip - hello varolan üstbilgi değeri değiştirmez.<br />-Ekle - hello değeri toohello varolan üstbilgi değeri ekler.<br />-delete - hello üstbilgisini hello isteğinden kaldırır.<br /><br /> Ayarlandığında çok`override` birden çok girişi kaydetme; hello ile aynı sonuçları (birden çok kez listelenir) kümesi according tooall girdisi olan hello üstbilgisinde adı yalnızca listelenen değerler hello sonucunda ayarlanır.|Hayır|geçersiz kılma|  
|ad|Merhaba üstbilgi toobe kümesinin adını belirtir.|Evet|Yok|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen, giden arka uç, hata  
  
-   **İlke kapsamları:** genel, ürün, API işlemi  
  
##  <a name="SetQueryStringParameter"></a>Set sorgu dizesi parametresi  
 Merhaba `set-query-parameter` ilkesi ekler, değiştirir değeri, veya silme isteği sorgu dizesi parametresi. Kullanılan toopass isteğe bağlı olan veya hiç hello istekte mevcut hello arka uç hizmeti tarafından beklenen sorgu parametreleri olabilir.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with hello same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a>Örnekler  
  
#### <a name="example"></a>Örnek  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with hello same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a>Bağlam bilgileri toohello arka uç hizmeti ilet  
 Bu örnek, tooapply İlkesi hello API düzey toosupply bağlam bilgileri toohello arka uç hizmetini nasıl gösterir. Yapılandırma ve bu ilkeyi kullanan bir örnek için bkz: [bulut kapak bölüm 177: daha Vlad Vinogradsky ile yönetim özelliklerini API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) ve too10:30 ileri sarma. 12:10 İşte hello İlkesi görebileceğiniz bir işlem hello Geliştirici Portalı'nda arama demo yoktur.  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward a piece of context, product name in this example, toohello backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 Daha fazla bilgi için bkz: [ilke ifadelerini](api-management-policy-expressions.md) ve [bağlamının](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="elements"></a>Öğeleri  
  
|Ad|Açıklama|Gerekli|  
|----------|-----------------|--------------|  
|kümesi sorgu parametresi|Kök öğesi.|Evet|  
|değer|Merhaba sorgu parametresi toobe kümesi Hello değerini belirtir. Merhaba ile birden çok sorgu parametreleri için aynı adı ekle ek `value` öğeleri.|Evet|  
  
### <a name="properties"></a>Özellikler  
  
|Ad|Açıklama|Gerekli|Varsayılan|  
|----------|-----------------|--------------|-------------|  
|Mevcut eylem|Merhaba sorgu parametresi zaten belirtildiğinde hangi eylemini tootake belirtir. Bu öznitelik değerlerini aşağıdaki hello birine sahip olmalıdır.<br /><br /> -değiştirir hello hello varolan parametresinin değerini geçersiz kıl -.<br />-skip - hello varolan sorgusu parametre değeri değiştirmez.<br />-Ekle - hello değeri toohello varolan sorgusu parametre değeri ekler.<br />-delete - hello sorgu parametresi hello isteğinden kaldırır.<br /><br /> Ayarlandığında çok`override` birden çok girişi kaydetme; hello ile aynı (birden çok kez listelenir) kümesi according tooall girdisi olan hello sorgu parametresi sonuçlarında adı yalnızca listelenen değerler hello sonucunda ayarlanır.|Hayır|geçersiz kılma|  
|ad|Merhaba sorgu parametresi toobe kümesinin adını belirtir.|Evet|Yok|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen, arka uç  
  
-   **İlke kapsamları:** genel, ürün, API işlemi  
  
##  <a name="RewriteURL"></a>URL yeniden yazma  
 Merhaba `rewrite-uri` ilkeyi dönüştürür istek URL'si hello web hizmeti tarafından beklenen genel form toohello formundan hello aşağıdaki örnekte gösterildiği gibi.  
  
-   Ortak URL-`http://api.example.com/storenumber/ordernumber`  
  
-   İstek URL-`http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`  
  
 Bu ilke, İnsan ve/veya tarayıcı kolay URL hello web hizmeti tarafından beklenen hello URL biçimine dönüştürülmesi gereken olduğunda kullanılabilir. Bu ilke, yalnızca temiz URL'leri, RESTful URL'leri, kullanıcı dostu URL'leri veya bir sorgu dizesi içermiyor ve bunun yerine yalnızca hello hello yolunu içeren zamanıyla ilgili yapısal URL'leri SEO dostu URL'leri gibi alternatif bir URL biçimi gösterme uygulanır toobe gerekir Kaynak (sonra hello şema ve hello yetkili). Bu genellikle estetik, kullanılabilirlik veya arama motoru iyileştirmesi (SEO) amacıyla yapılır.  
  
> [!NOTE]
>  Sorgu dizesi parametreleri hello İlkesi'ni kullanarak yalnızca ekleyebilirsiniz. Ek şablon yolu hello parametrelerinde URL yeniden yazma ekleyemezsiniz.  

### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a>Örnek  
  
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

### <a name="elements"></a>Öğeleri  
  
|Ad|Açıklama|Gerekli|  
|----------|-----------------|--------------|  
|yeniden yazma URI'sı|Kök öğesi.|Evet|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Öznitelik|Açıklama|Gerekli|Varsayılan|  
|---------------|-----------------|--------------|-------------|  
|şablon|herhangi bir sorgu dizesi parametre ile Merhaba gerçek web hizmeti URL'si. İfadeler kullanırken hello tam değeri bir ifade olmalıdır.|Evet|Yok|  
|kopya eşleşmeyen-parametreleri|Sorgu parametrelerini gelen istekteki hello hello özgün URL şablonunda mevcut değil hello tarafından tanımlanan toohello URL yeniden yazma şablon eklenip eklenmeyeceğini belirtir|Hayır|TRUE|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen  
  
-   **İlke kapsamları:** ürün, API işlemi  
  
##  <a name="XSLTransform"></a>XSLT kullanarak XML dönüştürme  
 Merhaba `Transform XML using an XSLT` ilke bir XSL Dönüştürme tooXML hello istek veya yanıt gövdesi içinde uygulanır.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
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
  
### <a name="example"></a>Örnek  
  
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
  
### <a name="elements"></a>Öğeleri  
  
|Ad|Açıklama|Gerekli|  
|----------|-----------------|--------------|  
|XSL Dönüştürme|Kök öğesi.|Evet|  
|Parametre|Merhaba dönüşüm dosyasında kullanılan kullanılan toodefine değişkenler|Hayır|  
|stylesheet|Kök stil öğesi. Tüm öğeleri ve özniteliklerinin içinde tanımlanan hello standarda [XSLT belirtimi](http://www.w3.org/TR/xslt)|Evet|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen, giden  
  
-   **İlke kapsamları:** genel, ürün, API işlemi  
  
## <a name="next-steps"></a>Sonraki adımlar
İlkeleriyle çalışma daha fazla bilgi için bkz: [API Management ilkeleri](api-management-howto-policies.md).  
