---
title: "aaaAzure API Management erişimi kısıtlama ilkeleri | Microsoft Docs"
description: "Merhaba erişim kısıtlama ilkeleri kullanılmak üzere Azure API Management hakkında bilgi edinin."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 034febe3-465f-4840-9fc6-c448ef520b0f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 0ef368c2781d9a5cf9eaaa41a47489c904ed3198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-access-restriction-policies"></a>API yönetim erişim kısıtlama ilkeleri
Bu konuda API Management ilkelere hello için bir başvuru sağlar. Ekleme ve ilkeleri yapılandırma hakkında daha fazla bilgi için bkz: [API Management ilkeleri](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="AccessRestrictionPolicies"></a>Erişimi kısıtlama ilkeleri  
  
-   [Onay HTTP üstbilgisi](api-management-access-restriction-policies.md#CheckHTTPHeader) -varlığı ve/veya bir HTTP üstbilgisi değerini zorlar.  
  
-   [Abonelik tarafından çağrı hızını sınırla](api-management-access-restriction-policies.md#LimitCallRate) -engeller API kullanımı ani başına abonelik başına çağrı hızını sınırlayarak.  
  
-   [Anahtara göre çağrı hızını sınırla](#LimitCallRateByKey) -engeller API kullanımı ani başına anahtar başına çağrı hızını sınırlayarak.  
  
-   [Arayan IP'leri kısıtlamak](api-management-access-restriction-policies.md#RestrictCallerIPs) -filtreleri (verir/engellediği) çağrılarından belirli IP adreslerini ve/veya adres aralığı.  
  
-   [Abonelik tarafından kullanım kotası ayarla](api-management-access-restriction-policies.md#SetUsageQuota) -bir abonelik başına temelinde tooenforce yenilenebilir veya ömrü çağrısı birim ve/veya bant genişliği kotaya izin verir.  
  
-   [Anahtara göre kullanım kotası ayarla](#SetUsageQuotaByKey) -bir anahtar başına temelinde tooenforce yenilenebilir veya ömrü çağrısı birim ve/veya bant genişliği kotaya izin verir.  
  
-   [JWT doğrulama](api-management-access-restriction-policies.md#ValidateJWT) -varlığı ve belirtilen bir HTTP üstbilgisi veya belirtilen sorgu parametresi ayıklanan JWT geçerliliğini zorlar.  
  
##  <a name="CheckHTTPHeader"></a>HTTP üstbilgisi denetleyin  
 Kullanım hello `check-header` İlkesi tooenforce bir istek belirtilen bir HTTP üstbilgisi vardır. Belirli bir değer veya izin verilen değer aralığı için onay Hello üstbilgi varsa, isteğe bağlı olarak toosee kontrol edebilirsiniz. Merhaba denetimi başarısız olursa hello İlkesi isteği işleme sonlandırır ve hello İlkesi tarafından belirtilen hello HTTP durum kodu ve hata iletisi döndürür.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a>Örnek  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a>Öğeleri  
  
|Ad|Açıklama|Gerekli|  
|----------|-----------------|--------------|  
|onay üstbilgisi|Kök öğesi.|Evet|  
|değer|İzin verilen HTTP üstbilgisi değeri. Birden çok değer öğesi belirtildiğinde, herhangi bir hello değerlerin bir eşleşme varsa hello onay başarı olarak kabul edilir.|Hayır|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Ad|Açıklama|Gerekli|Varsayılan|  
|----------|-----------------|--------------|-------------|  
|başarısız oldu-onay-hata iletisi|Hata iletisi tooreturn hello üstbilgi yok veya geçersiz bir değere sahip olursa hello HTTP yanıt gövdesi içinde. Bu ileti, tüm özel karakterleri düzgün şekilde çıkıldığından olması gerekir.|Evet|Yok|  
|başarısız oldu-onay-httpcode|HTTP durum kodu tooreturn Hello üstbilgi yok veya geçersiz bir değere sahip.|Evet|Yok|  
|üstbilgi adı|Merhaba HTTP üstbilgisi toocheck Hello adı.|Evet|Yok|  
|Yoksay durumu|TooTrue ya da yanlış ayarlanmış olabilir. Merhaba üstbilgi değeri kabul edilebilir değerler hello kümesi karşı karşılaştırıldığında kümesi tooTrue durum göz ardı gerekiyorsa.|Evet|Yok|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen, giden  
  
-   **İlke kapsamları:** genel, ürün, API işlemi  
  
##  <a name="LimitCallRate"></a>Abonelik tarafından çağrı hızını sınırla  
 Merhaba `rate-limit` ilke engeller API kullanımı ani hello sınırlayarak abonelik başına temelinde oranı tooa belirtilen belirli bir süre sayı çağırın. Bu ilke tetiklendiğinde hello arayan alan bir `429 Too Many Requests` yanıt durum kodu.  
  
> [!IMPORTANT]
>  Bu ilke, ilke belge başına yalnızca bir kez kullanılabilir.  
>   
>  [İlke ifadeleri](api-management-policy-expressions.md) hello İlkesi özniteliklerini hiçbirinde Bu ilke için kullanılamaz.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a>Örnek  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit calls="20" renewal-period="90" />  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Öğeleri  
  
|Ad|Açıklama|Gerekli|  
|----------|-----------------|--------------|  
|sınırını ayarlama|Kök öğesi.|Evet|  
|api|Bir veya daha fazla bu öğeleri tooimpose çağrı hızı sınırı API'leri hello ürün içinde ekleyin. Ürün ve API sınırları bağımsız olarak uygulanır oranı arayın.|Hayır|  
|işlemi|Bir veya daha fazla bu öğeleri tooimpose çağrı hızı sınırı bir API işlemlerini ekleyin. Ürün, API ve işlem sınırları bağımsız olarak uygulanır oranı çağırın.|Hayır|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Ad|Açıklama|Gerekli|Varsayılan|  
|----------|-----------------|--------------|-------------|  
|ad|hangi tooapply hello hızı sınırı hello API adı Hello.|Evet|Yok|  
|çağrıları|Merhaba çağrıları hello belirtilen hello zaman aralığı boyunca izin verilen en fazla toplam sayısı `renewal-period`.|Evet|Yok|  
|yenileme dönemi|Merhaba zaman aralığını saniye olarak geçmesi hello kota sıfırlar.|Evet|Yok|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen  
  
-   **İlke kapsamları:** ürün  
  
##  <a name="LimitCallRateByKey"></a>Anahtara göre çağrı hızını sınırla  
 Merhaba `rate-limit-by-key` ilke engeller API kullanımı ani hello sınırlayarak anahtar başına temelinde oranı tooa belirtilen belirli bir süre sayı çağırın. Merhaba anahtar bir isteğe bağlı bir dize değerine sahip olabilir ve genellikle bir ilke ifade kullanılarak sağlanır. İsteğe bağlı increment koşulu, hangi isteklerinin hello sınırında sayılması toospecify eklenebilir. Bu ilke tetiklendiğinde hello arayan alan bir `429 Too Many Requests` yanıt durum kodu.  
  
 Daha fazla bilgi ve bu ilkeyi örnekleri için bkz: [Gelişmiş istek azaltma Azure API Management ile](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).  
  
> [!IMPORTANT]
>  Bu ilke, ilke belge başına yalnızca bir kez kullanılabilir.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a>Örnek  
 Aşağıdaki örneğine hello hello hızı sınırı hello arayan IP adresine göre anahtarlanır.  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit-by-key  calls="10"  
              renewal-period="60"  
              increment-condition="@(context.Response.StatusCode == 200)"  
              counter-key="@(context.Request.IpAddress)"/>  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Öğeleri  
  
|Ad|Açıklama|Gerekli|  
|----------|-----------------|--------------|  
|sınırını ayarlama|Kök öğesi.|Evet|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Ad|Açıklama|Gerekli|Varsayılan|  
|----------|-----------------|--------------|-------------|  
|çağrıları|Merhaba çağrıları hello belirtilen hello zaman aralığı boyunca izin verilen en fazla toplam sayısı `renewal-period`.|Evet|Yok|  
|Tamamlayıcı anahtarı|Merhaba hello hız sınırı ilkesi için anahtar toouse.|Evet|Yok|  
|Koşul artırma|Merhaba isteği hello kota sayılan olmadığını belirten hello Boole ifadesi (`true`).|Hayır|Yok|  
|yenileme dönemi|Merhaba zaman aralığını saniye olarak geçmesi hello kota sıfırlar.|Evet|Yok|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen  
  
-   **İlke kapsamları:** genel, ürün, API işlemi  
  
##  <a name="RestrictCallerIPs"></a>Arayan IP'leri kısıtla  
 Merhaba `ip-filter` ilke filtrelerini belirli IP adreslerini ve/veya adres aralıklarını gelen çağrıları (verir/engeller).  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a>Örnek  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a>Öğeleri  
  
|Ad|Açıklama|Gerekli|  
|----------|-----------------|--------------|  
|IP Filtresi|Kök öğesi.|Evet|  
|Adres|Tek bir IP adresi üzerinde hangi toofilter belirtir.|En az bir `address` veya `address-range` öğesi gereklidir.|  
|adres aralığı adresinden ="" için "Adres" =|Bir IP adresi aralığı üzerinde hangi toofilter belirtir.|En az bir `address` veya `address-range` öğesi gereklidir.|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Ad|Açıklama|Gerekli|Varsayılan|  
|----------|-----------------|--------------|-------------|  
|adres aralığı adresinden ="" için "Adres" =|Bir dizi IP tooallow adresleri veya erişimi reddetmek.|Merhaba gereklidir `address-range` öğe kullanılır.|Yok|  
|IP filtre eylemi = "izin &#124; yasaklamaz"|Çağrıları izin verilmesi veya IP adresleri ve aralıkları değil hello için belirtilen olup olmadığını belirtir.|Evet|Yok|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen  
  
-   **İlke kapsamları:** genel, ürün, API işlemi  
  
##  <a name="SetUsageQuota"></a>Abonelik tarafından kullanım kotası ayarla  
 Merhaba `quota` ilke yenilenebilir veya ömrü çağrısı birim ve/veya bant genişliği kota, abonelik başına temelinde zorunlu tutar.  
  
> [!IMPORTANT]
>  Bu ilke, ilke belge başına yalnızca bir kez kullanılabilir.  
>   
>  [İlke ifadeleri](api-management-policy-expressions.md) hello İlkesi özniteliklerini hiçbirinde Bu ilke için kullanılamaz.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a>Örnek  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota calls="10000" bandwidth="40000" renewal-period="3600" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Öğeleri  
  
|Ad|Açıklama|Gerekli|  
|----------|-----------------|--------------|  
|Kota|Kök öğesi.|Evet|  
|api|Bir veya daha fazla bu öğeleri tooimpose kota API'leri hello ürün içinde ekleyin. Ürün ve API kotaları bağımsız olarak uygulanır.|Hayır|  
|işlemi|Bir veya daha fazla bu öğeleri tooimpose kota bir API işlemlerini ekleyin. Ürün, API ve işlem kotaları bağımsız olarak uygulanır.|Hayır|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Ad|Açıklama|Gerekli|Varsayılan|  
|----------|-----------------|--------------|-------------|  
|ad|Merhaba adı hello API veya işlemi için hangi hello kota uygulanır.|Evet|Yok|  
|Bant genişliği|Merhaba kilobayt hello belirtilen hello zaman aralığı boyunca izin verilen en fazla toplam sayısı `renewal-period`.|Her iki `calls`, `bandwidth`, veya her ikisini de birlikte belirtilmesi gerekir.|Yok|  
|çağrıları|Merhaba çağrıları hello belirtilen hello zaman aralığı boyunca izin verilen en fazla toplam sayısı `renewal-period`.|Her iki `calls`, `bandwidth`, veya her ikisini de birlikte belirtilmesi gerekir.|Yok|  
|yenileme dönemi|Merhaba zaman aralığını saniye olarak geçmesi hello kota sıfırlar.|Evet|Yok|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen  
  
-   **İlke kapsamları:** ürün  
  
##  <a name="SetUsageQuotaByKey"></a>Anahtara göre kullanım kotası ayarla  
 Merhaba `quota-by-key` ilke yenilenebilir veya ömrü çağrısı birim ve/veya bant genişliği kota anahtarı başına temelinde zorunlu tutar. Merhaba anahtar bir isteğe bağlı bir dize değerine sahip olabilir ve genellikle bir ilke ifade kullanılarak sağlanır. İsteğe bağlı increment koşulu, hangi istekler hello kota sayılması toospecify eklenebilir.  
  
 Daha fazla bilgi ve bu ilkeyi örnekleri için bkz: [Gelişmiş istek azaltma Azure API Management ile](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).  
  
> [!IMPORTANT]
>  Bu ilke, ilke belge başına yalnızca bir kez kullanılabilir.  
>   
>  [İlke ifadeleri](api-management-policy-expressions.md) hello İlkesi özniteliklerini hiçbirinde Bu ilke için kullanılamaz.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a>Örnek  
 Aşağıdaki örneğine hello hello kota hello arayan IP adresine göre anahtarlanır.  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota-by-key calls="10000" bandwidth="40000" renewal-period="3600"  
                      increment-condition="@(context.Response.StatusCode >= 200 && context.Response.StatusCode < 400)"  
                      counter-key="@(context.Request.IpAddress)" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Öğeleri  
  
|Ad|Açıklama|Gerekli|  
|----------|-----------------|--------------|  
|Kota|Kök öğesi.|Evet|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Ad|Açıklama|Gerekli|Varsayılan|  
|----------|-----------------|--------------|-------------|  
|Bant genişliği|Merhaba kilobayt hello belirtilen hello zaman aralığı boyunca izin verilen en fazla toplam sayısı `renewal-period`.|Her iki `calls`, `bandwidth`, veya her ikisini de birlikte belirtilmesi gerekir.|Yok|  
|çağrıları|Merhaba çağrıları hello belirtilen hello zaman aralığı boyunca izin verilen en fazla toplam sayısı `renewal-period`.|Her iki `calls`, `bandwidth`, veya her ikisini de birlikte belirtilmesi gerekir.|Yok|  
|Tamamlayıcı anahtarı|Merhaba hello kota ilkesi için anahtar toouse.|Evet|Yok|  
|Koşul artırma|Merhaba isteği hello kota sayılan olmadığını belirten hello Boole ifadesi (`true`)|Hayır|Yok|  
|yenileme dönemi|Merhaba zaman aralığını saniye olarak geçmesi hello kota sıfırlar.|Evet|Yok|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen  
  
-   **İlke kapsamları:** genel, ürün, API işlemi  
  
##  <a name="ValidateJWT"></a>JWT doğrula  
 Merhaba `validate-jwt` İlkesi varlığı zorunlu kılan ve HTTP üstbilgisi veya belirtilen sorgu parametresi JWT geçerliliğini ya da belirtilen bir ayıklanır.  
  
> [!IMPORTANT]
>  Merhaba `validate-jwt` ilke gerektiriyorsa Bu hello `exp` kayıtlı talep olduğu hello JWT belirteci inlcuded sürece `require-expiration-time` öznitelik belirtilen ve çok ayarlayın`false`.  
> Merhaba `validate-jwt` İlkesi HS256 ve RS256 imza algoritmaları destekler. HS256 için başlangıç anahtarı hello İlkesi'nde hello base64 ile kodlanmış form içi sağlanmalıdır. RS256 için bir Open ID yapılandırma uç noktası aracılığıyla sağlamak toobe hello anahtarı yok.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<validate-jwt   
    header-name="name of http header containing hello token (use query-parameter-name attribute if hello token is passed in hello URL)"   
    failed-validation-httpcode="http status code tooreturn on failure"   
    failed-validation-error-message="error message tooreturn on failure"   
    require-expiration-time="true|false"
    require-scheme="scheme"
    require-signed-tokens="true|false"   
    clock-skew="allowed clock skew in seconds">  
  <issuer-signing-keys>  
    <key>base64 encoded signing key</key>  
    <!-- if there are multiple keys, then add additional key elements -->  
  </issuer-signing-keys>  
  <audiences>  
    <audience>audience string</audience>  
    <!-- if there are multiple possible audiences, then add additional audience elements -->  
  </audiences>  
  <issuers>  
    <issuer>issuer string</issuer>  
    <!-- if there are multiple possible issuers, then add additional issuer elements -->  
  </issuers>  
  <required-claims>  
    <claim name="name of hello claim as it appears in hello token" match="all|any">  
      <value>claim value as it is expected tooappear in hello token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of hello configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a>Örnekler  
  
#### <a name="azure-mobile-services-token-validation"></a>Azure Mobile Services belirteci doğrulama  
  
```xml  
<validate-jwt header-name="x-zumo-auth" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Supplied access token is invalid.">  
    <issuers>  
        <issuer>urn:microsoft:windows-azure:zumo</issuer>  
    </issuers>  
    <audiences>  
        <audience>Facebook</audience>  
    </audiences>  
    <issuer-signing-keys>  
        <zumo-master-key id="0">insert key here</zumo-master-key>  
    </issuer-signing-keys>  
</validate-jwt>  
```  
  
#### <a name="azure-active-directory-token-validation"></a>Azure Active Directory token doğrulama  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration" />  
    <audiences>
        <audience>25eef6e4-c905-4a07-8eb4-0d08d5df8b3f</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  

  
#### <a name="azure-active-directory-b2c-token-validation"></a>Azure Active Directory B2C belirteç doğrulama  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/tfp/contoso.onmicrosoft.com/b2c_1_signin/v2.0/.well-known/openid-configuration" />
    <audiences>
        <audience>d313c4e4-de5f-4197-9470-e509a2f0b806</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  
  
#### <a name="authorize-access-toooperations-based-on-token-claims"></a>Belirteç taleplerine dayalı erişim toooperations yetkilendirmek  
 Bu örnek gösterir nasıl toouse hello [JWT doğrulamak](api-management-access-restriction-policies.md#ValidateJWT) İlkesi toopre-belirteci taleplerine dayalı erişim toooperations yetkilendirin. Yapılandırma ve bu ilkeyi kullanan bir örnek için bkz: [bulut kapak bölüm 177: daha Vlad Vinogradsky ile yönetim özelliklerini API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) ve too13:50 ileri sarma. Too15:00 hello İlkesi Düzenleyicisi'nde yapılandırılan toosee hello İlkesi sarma ve ardından yetkilendirme belirtecini too18:50 hem ile hem de hello olmadan hello Geliştirici Portalı'ndan bir işlem çağırma, bir örnek için gerekli.  
  
```xml  
<!-- Copy hello following snippet into hello inbound section at hello api (or higher) level toopre-authorize access toooperations based on token claims -->  
<set-variable name="signingKey" value="insert signing key here" />  
<choose>  
  <when condition="@(context.Request.Method.Equals("patch",StringComparison.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="edit">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <when condition="@(new [] {"post", "put"}.Contains(context.Request.Method,StringComparer.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="create">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <otherwise>  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
    </validate-jwt>  
  </otherwise>  
</choose>  
```  
  
### <a name="elements"></a>Öğeleri  
  
|Öğesi|Açıklama|Gerekli|  
|-------------|-----------------|--------------|  
|doğrulama jwt|Kök öğesi.|Evet|  
|Hedef kitle|Merhaba belirteçte mevcut olabilecek kabul edilebilir İzleyici talep listesini içerir. Birden fazla hedef kitle değer mevcut sonra her değer denenir kadar tüm (Bu durumda doğrulama başarısız) tükendiği veya biri başarılı olana kadar. En az bir hedef kitle belirtilmelidir.|Hayır|  
|verici İmzalama anahtarları|Base64 ile kodlanmış güvenlik kullanılan anahtarları toovalidate listesini belirteçleri imzalanmış. Birden çok güvenlik anahtarları varsa sonra her anahtar denenir kadar tüm (Bu durumda doğrulama başarısız) tükendiği veya biri (belirteci geçiş işlemi için yararlıdır) başarılı olana kadar. Anahtar öğeleri sahip isteğe bağlı bir `id` kullanılan öznitelik toomatch karşı `kid` talep.|Hayır|  
|verenler|Merhaba belirteç kabul edilebilir sorumluların listesini. Birden çok veren değer mevcut sonra her değer denenir kadar tüm (Bu durumda doğrulama başarısız) tükendiği veya biri başarılı olana kadar.|Hayır|  
|openıd-config|içinden İmzalama anahtarları ve veren alınabilir uyumlu bir Open ID yapılandırma endpoint belirtmek için kullanılan hello öğe.|Hayır|  
|gerekli talep|Geçerli olarak kabul toobe beklenen talep toobe için hello belirteçte mevcut listesini içerir. Ne zaman hello `match` özniteliği olarak ayarlanmış çok`all` hello İlkesi'nde her talep değeri için doğrulama toosucceed hello belirteçte mevcut olması gerekir. Ne zaman hello `match` özniteliği olarak ayarlanmış çok`any` en az bir talep doğrulama toosucceed hello belirteçte mevcut olmalıdır.|Hayır|  
|zumo ana anahtarı|Ana anahtar için Azure Mobile Services tarafından yayınlanan belirteçleri|Hayır|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Ad|Açıklama|Gerekli|Varsayılan|  
|----------|-----------------|--------------|-------------|  
|saat eğriltme|TimeSpan. Merhaba belirtecinin süre sonu talep hello belirteçte ve hello geçerli durumda bazı küçük leeway sağlar tarih / saat.|Hayır|0 saniye|  
|başarısız oldu-doğrulama-hata iletisi|Hata iletisi tooreturn hello JWT doğrulamayı geçemezse hello HTTP yanıt gövdesi içinde. Bu ileti, tüm özel karakterleri düzgün şekilde çıkıldığından olması gerekir.|Hayır|Varsayılan hata iletisini doğrulama sorunu, örneğin "JWT mevcut değil." bağlıdır|  
|başarısız oldu-doğrulama-httpcode|HTTP durum kodu tooreturn Hello JWT doğrulamayı geçerse değil.|Hayır|401|  
|üstbilgi adı|Merhaba belirteci bulunduran hello HTTP üstbilgisinin Hello adı.|Ya da `header-name` veya `query-paremeter-name` belirtilmelidir; ancak ikisi birden değil.|Yok|  
|id|Merhaba `id` hello öznitelikte `key` öğesi karşı eşleşen toospecify hello dize verir `kid` hello (varsa) belirteci toofind hello uygun anahtar toouse imza doğrulaması için giden talep.|Hayır|Yok|  
|eşleşme|Merhaba `match` hello öznitelikte `claim` öğesi hello İlkesi'nde her talep değeri için doğrulama toosucceed hello belirteçte mevcut olup olmadığını belirtir. Olası değerler şunlardır:<br /><br /> -                          `all`-hello İlkesi'nde her talep değeri için doğrulama toosucceed hello belirteçte mevcut olması gerekir.<br /><br /> -                          `any`-en az bir talep değeri için doğrulama toosucceed hello belirteçte mevcut olmalıdır.|Hayır|Tüm|  
|Sorgu paremeter adı|Merhaba belirteci bulunduran hello hello sorgu parametresi Hello adı.|Ya da `header-name` veya `query-paremeter-name` belirtilmelidir; ancak ikisi birden değil.|Yok|  
|gerekli-sona erme-time|Boole değeri. Bir süre sonu talep hello belirteçte gerekip gerekmediğini belirtir.|Hayır|TRUE|
|gerektiren düzeni|Merhaba belirteci Hello adını düzen, örn. "Bearer". Bu öznitelik ayarlandığında hello İlkesi düzeni hello kimlik doğrulaması üstbilgi değeri mevcut belirtilen güvence altına alır.|Hayır|Yok|
|gerekli-oturum-belirteçleri|Boole değeri. Bir belirteç imzalı gerekli toobe olup olmadığını belirtir.|Hayır|TRUE|  
|URL|Burada Open ID yapılandırma meta verilerini elde edilebilir gelen kimliği yapılandırma uç noktasının URL'sini açın. Azure Active Directory için URL aşağıdaki hello kullan: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` directory Kiracı adınız, örneğin değiştirerek `contoso.onmicrosoft.com`.|Evet|Yok|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen  
  
-   **İlke kapsamları:** genel, ürün, API işlemi  
  
## <a name="next-steps"></a>Sonraki adımlar
İlkeleriyle çalışma daha fazla bilgi için bkz: [API Management ilkeleri](api-management-howto-policies.md).  
