---
title: "Azure API Management ilkeleri işleme aaaError | Microsoft Docs"
description: "Azure API Management'te isteklerinin işlenmesi sırasında oluşabilecek toorespond tooerror koşullar nasıl hello öğrenin."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 3c777964-02b2-4f55-8731-8c3bd3c0ae27
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 002c65f21e763fd644da61b6a11685ffd97488c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="error-handling-in-api-management-policies"></a>API Management ilkeleri işleme hatası
Azure API Management sağlayarak istekleri toohello proxy hello işlenmesi sırasında ortaya çıkabilecek toorespond tooerror koşullar yayımcılar sağlayan bir `ProxyError` nesnesi. Merhaba `ProxyError` nesne hello erişilen [bağlamı. Son hata](api-management-policy-expressions.md#ContextVariables) özelliği ve hello ilkeleri tarafından kullanılan `on-error` ilke bölümü. Bu konuda bir başvuru hello hatası için Azure API Management'te işleme yetenekleri sağlar.  
  
## <a name="error-handling-in-api-management"></a>API Management'te işleme hatası  
 Azure API Management ilkeleri uygulamasına bölünen `inbound`, `backend`, `outbound`, ve `on-error` bölümler hello aşağıdaki örnekte gösterildiği gibi.  
  
```xml  
<policies>  
  <inbound>  
    <!-- statements toobe applied toohello request go here -->  
  </inbound>  
  <backend>  
    <!-- statements toobe applied before hello request is   
         forwarded toohello backend service go here -->  
    </backend>  
    <outbound>  
      <!-- statements toobe applied toohello response go here -->  
    </outbound>  
    <on-error>  
        <!-- statements toobe applied if there is an error   
             condition go here -->  
  </on-error>  
</policies>  
```  
  
 Bir istek Hello işlenirken hello istek için kapsamdaki tüm ilkeleri ile birlikte yerleşik adımları yürütülür. Bir hata oluşursa, hemen işleme toohello atlar `on-error` ilke bölümü. Merhaba `on-error` İlkesi bölümünde herhangi bir kapsamda kullanılabilir ve API yayımcılar hello hata tooevent hub günlüğü veya yeni bir yanıt tooreturn toohello çağıran oluşturma gibi özel davranışını yapılandırabilir.  
  
> [!NOTE]
>  Merhaba `on-error` bölümü ilkeleri varsayılan olarak mevcut değil. tooadd hello `on-error` bölümünde tooa İlkesi, istenen toohello İlkesi'nde hello İlkesi Düzenleyicisi'ni bulun ve ekleyin. İlkeleri yapılandırma hakkında daha fazla bilgi için bkz: [API Management ilkeleri](https://azure.microsoft.com/documentation/articles/api-management-howto-policies/).  
>   
>  Varsa hiçbir `on-error` bölümünde arayanlar alacağı 400 veya 500 HTTP yanıt iletilerini bir hata koşulu ortaya çıkarsa.  
  
### <a name="policies-allowed-in-on-error"></a>Üzerinde hatada izin ilkeleri  
 Merhaba aşağıdaki ilkeleri hello kullanılabilir `on-error` ilke bölümü.  
  
-   [seçin](api-management-advanced-policies.md#choose)  
  
-   [değişken Ayarla](api-management-advanced-policies.md#set-variable)  
  
-   [Bul ve Değiştir](api-management-transformation-policies.md#Findandreplacestringinbody)  
  
-   [return yanıt](api-management-advanced-policies.md#ReturnResponse)  
  
-   [set üstbilgisi](api-management-transformation-policies.md#SetHTTPheader)  
  
-   [Set yöntemi](api-management-advanced-policies.md#SetRequestMethod)  
  
-   [durumunu ayarla](api-management-advanced-policies.md#SetStatus)  
  
-   [Gönderme isteği](api-management-advanced-policies.md#SendRequest)  
  
-   [bir şekilde İsteği Gönder](api-management-advanced-policies.md#SendOneWayRequest)  
  
-   [Günlük eventhub](api-management-advanced-policies.md#log-to-eventhub)  
  
-   [JSON xml](api-management-transformation-policies.md#ConvertJSONtoXML)  
  
-   [XML json](api-management-transformation-policies.md#ConvertXMLtoJSON)  
  
## <a name="lasterror"></a>Son hata  
 Ne zaman bir hata oluşur ve denetim atlar toohello `on-error` İlkesi bölümünde hello hata depolanır [bağlamı. Son hata](api-management-policy-expressions.md#ContextVariables) hello ilkelerinde tarafından erişilen özellik `on-error` bölümünde ve hello aşağıdaki özelliklere sahiptir.  
  
|Ad|Tür|Açıklama|Gerekli|  
|----------|----------|-----------------|--------------|  
|Kaynak|Dize|Merhaba hatanın oluştuğu adları hello öğesi. İlke veya yerleşik ardışık düzen adım adı olabilir.|Evet|  
|Neden|Dize|Hata işleme kullanılabilir makine kolay hata kodu.|Hayır|  
|İleti|Dize|Okunabilir hata açıklaması.|Evet|  
|Kapsam|Dize|Burada hello hata oluştu ve "Genel", "Ürün", "API" veya "işlem" biri olabilir hello kapsam adı|Hayır|  
|Bölüm|Dize|Burada bir hata oluştu ve aşağıdakilerden birini "gelen" bölüm adı, "arka uç", "giden" veya "hata".|Hayır|  
|Yol|Dize|İç içe geçmiş İlkesi, örneğin belirtir "[3] seçin / ne zaman [2]".|Hayır|  
|Policyıd|Dize|Merhaba değerini `id` hatanın oluştuğu hello ilkedeki hello müşteri tarafından belirtilmişse özniteliği|Hayır|  
  
> [!NOTE]
>  Tüm ilkeler isteğe sahip `id` hello İlkesi toohello kök öğesi eklenebilir özniteliği. Bir hata koşulu oluştuğunda bu öznitelik bir ilke varsa, hello özniteliğinin hello değeri hello kullanılarak alınabilir `context.LastError.PolicyId` özelliği.  
  
## <a name="predefined-errors-for-built-in-steps"></a>Yerleşik adımlar için önceden tanımlanmış hataları  
 Merhaba aşağıdaki hataları yerleşik işleme adımları hello değerlendirme sırasında ortaya çıkabilecek hata koşulları için önceden tanımlanmıştır.  
  
|Kaynak|Koşul|Neden|İleti|  
|------------|---------------|------------|-------------|  
|yapılandırma|URI tooany API veya işlemi eşleşmiyor|OperationNotFound|%S toomatch gelen istek tooan işlemi.|  
|Yetkilendirme|Abonelik anahtarı sağlanmadı|SubscriptionKeyNotFound|Erişim toomissing abonelik anahtarı reddedildi. Emin tooinclude abonelik anahtarı isteklerini toothis API yaparken olun.|  
|Yetkilendirme|Abonelik anahtarı değeri geçersiz|SubscriptionKeyInvalid|Erişim tooinvalid abonelik anahtarı reddedildi. Etkin bir aboneliğiniz için geçerli bir anahtar tooprovide emin olun.|  
  
## <a name="predefined-errors-for-policies"></a>İlkeleri için önceden tanımlanmış hataları  
 Merhaba aşağıdaki hataları İlkesi değerlendirmesi sırasında ortaya çıkabilecek hata koşulları için önceden tanımlanmıştır.  
  
|Kaynak|Koşul|Neden|İleti|  
|------------|---------------|------------|-------------|  
|hız sınırı|Hızı sınırı aşıldı|RateLimitExceeded|Hız sınırı aşıldı|  
|Kota|Kotası aşıldı|QuotaExceeded|Çağrı hacmi kotası aşıldı. Kota xx:xx:xx içinde yenilenmesi. - veya - bant genişliği kota dışında. Kota xx:xx:xx içinde yenilenmesi.|  
|jsonp|Geri çağırma parametresi değeri geçersiz (hatalı karakterler içerir)|CallbackParameterInvalid|{Geri arama parametresi adı} geri çağırma parametresinin değeri geçerli bir JavaScript tanımlayıcısı değil.|  
|IP Filtresi|İstek başarısız tooparse arayan IP|FailedToParseCallerIP|Tooestablish IP adresi hello çağıran için başarısız oldu. Erişim reddedildi.|  
|IP Filtresi|Arayan IP içinde değil izin verilen listesine|CallerIpNotAllowed|Arayan IP adresi {IP adresi} izin verilmiyor. Erişim reddedildi.|  
|IP Filtresi|Arayan IP Engellenenler listesinde değil|CallerIpBlocked|Arayan IP adresi engellendi. Erişim reddedildi.|  
|onay üstbilgisi|Gerekli üstbilgisi değil sunulan veya değer eksik|HeaderNotFound|Üstbilgi {üstbilgi-adı} hello istekte bulunamadı. Erişim reddedildi.|  
|onay üstbilgisi|Gerekli üstbilgisi değil sunulan veya değer eksik|HeaderValueNotAllowed|{Üstbilgi değeri} {üstbilgi-adı} üstbilgi değerini izin verilmiyor. Erişim reddedildi.|  
|doğrulama jwt|Jwt belirteci istekte eksik.|TokenNotFound|JWT Hello istekte bulunamadı. Erişim reddedildi.|  
|doğrulama jwt|İmza doğrulaması başarısız oldu|TokenSignatureInvalid|< İleti jwt kitaplığından\>. Erişim reddedildi.|  
|doğrulama jwt|Geçersiz hedef kitle|TokenAudienceNotAllowed|< İleti jwt kitaplığından\>. Erişim reddedildi.|  
|doğrulama jwt|Geçersiz veren|TokenIssuerNotAllowed|< İleti jwt kitaplığından\>. Erişim reddedildi.|  
|doğrulama jwt|Belirtecin süresi|TokenExpired|< İleti jwt kitaplığından\>. Erişim reddedildi.|  
|doğrulama jwt|İmza anahtarı kimliğine göre çözümlenemedi|TokenSignatureKeyNotFound|< İleti jwt kitaplığından\>. Erişim reddedildi.|  
|doğrulama jwt|Gerekli talepleri belirtecinden eksik|TokenClaimNotFound|JWT belirteci talepler aşağıdaki hello eksik: < c1\>, < c2\>,... Erişim reddedildi.|  
|doğrulama jwt|Talep değerleri eşleşmiyor|TokenClaimValueNotAllowed|{Talep değeri} {talep-adı} talep değeri izin verilmiyor. Erişim reddedildi.|  
|doğrulama jwt|Diğer doğrulama hataları|JwtInvalid|< İleti jwt kitaplığı\>|

## <a name="next-steps"></a>Sonraki adımlar
İlkeleriyle çalışma daha fazla bilgi için bkz: [API Management ilkeleri](api-management-howto-policies.md).  