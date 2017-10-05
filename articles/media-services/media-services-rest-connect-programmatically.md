---
title: "REST API kullanarak Media Services hesabına bağlanma | Microsoft Docs"
description: "Bu konu, Media Services kullanarak REST API bağlanmak gösterilmiştir."
services: media-services
documentationcenter: 
author: Juliako
manager: erikre
editor: 
ms.assetid: 79dc64f1-15d8-4a81-b9d9-3d3c44d2e1e8
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 4feb0eb81823835e8e0b701463d85b27f5598019
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connecting-to-media-services-account-using-media-services-rest-api"></a>Media Services REST API kullanarak Media Services hesabına bağlanma
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-connect-programmatically.md)
> * [REST](media-services-rest-connect-programmatically.md)
> 
> 

Bu konu, Media Services REST API ile programlama yaparken Microsoft Azure Media Services programlama bağlantı elde açıklar.

Microsoft Azure Media Services erişirken iki şey gereklidir: Azure erişim denetimi Hizmetleri (ACS) ve Media Services URI tarafından kendisine sağlanan bir erişim belirteci. Bu istekler doğru üstbilgi değerlerini belirtin ve Media Services'e çağırırken doğru erişim belirtecinde yer geçirin sürece oluştururken, istediğiniz herhangi bir yöntem kullanabilirsiniz.

Aşağıdaki adımlar, Media Services'e bağlanmak için Media Services REST API kullanırken en yaygın iş akışını açıklar:

1. Bir erişim belirteci alma 
2. URI Media Services'e bağlanma 
   
   > [!NOTE]
   > Başarıyla https://media.windows.net için bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız. Yeni bir URI yapılan sonraki çağrılar yapmanız gerekir.
   > ODATA API meta veri açıklamasını içeren bir HTTP/1.1 200 yanıtı de alabilirsiniz.
   > 
   > 
3. Yeni URL, sonraki API çağrıları gönderin. 
   
    Örneğin, bağlanmaya varsa sonra aşağıdaki aldığınız:
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    Sonraki API aramalarınız https://wamsbayclus001rest-hs.cloudapp.net/api/ göndermeniz gerekir.

    >[!NOTE]
    >Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için). Uzun süre boyunca kullanılmak için oluşturulan bulucu ilkeleri gibi aynı günleri / erişim izinlerini sürekli olarak kullanıyorsanız, aynı ilke kimliğini kullanmalısınız (karşıya yükleme olmayan ilkeler için). Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.

## <a name="access-control-address"></a>Erişim denetimi adresi
Media Services erişim denetimi https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn olduğu Kuzey Çin bölgesi dışında https://wamsprodglobal001acs.accesscontrol.windows.net adresidir.

## <a name="getting-an-access-token"></a>Bir erişim belirteci alma
Media Services REST API aracılığıyla doğrudan erişmek için ACS bir erişim belirteci almak ve hizmete yaptığınız her HTTP isteği sırasında kullanın. Bu belirteç, bir HTTP isteği ve OAuth v2 protokolünü kullanarak üstbilgisinde sağlanan erişim talepler bağlı ACS tarafından sağlanan diğer belirteçleri benzerdir. Herhangi bir önkoşulu Media Services'e doğrudan bağlanmadan önce gerekmez.

Aşağıdaki örnek HTTP istek üstbilgisi ve bir belirteç almak için kullanılan gövde gösterir.

**Üstbilgi**:

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


**Gövde**:

Bu istek gövdesinde client_id ve client_secret değerleri kanıtlamanız gerekir; AccountName ve AccountKey değerleri için sırasıyla client_id ve client_secret karşılık gelir. Hesabınızı ayarladığınızda, bu değerler, Media Services tarafından sağlanır. 

Media Services hesabınızı AccountKey URL kodlanmış olması gerektiğini unutmayın (bkz [yüzde kodlama](http://tools.ietf.org/html/rfc3986#section-2.1) erişim belirteci isteğiniz client_secret değer olarak kullanırken.

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


Örneğin: 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


Aşağıdaki örnek erişimi içeren HTTP yanıtı yanıt gövdesinde belirteci gösterir.

    HTTP/1.1 200 OK
    Cache-Control: no-cache, no-store
    Pragma: no-cache
    Content-Type: application/json; charset=utf-8
    Expires: -1
    request-id: a65150f5-2784-4a01-a4b7-33456187ad83
    X-Content-Type-Options: nosniff
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 15 Jan 2015 08:07:20 GMT
    Content-Length: 670

    {  
       "token_type":"http://schemas.xmlsoap.org/ws/2009/11/swt-token-profile-1.0",
       "access_token":"http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421330840&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=uf69n82KlqZmkJDNxhJkOxpyIpA2HDyeGUTtSnq1vlE%3d",
       "expires_in":"21600",
       "scope":"urn:WindowsAzureMediaServices"
    }


> [!NOTE]
> Bir dış depolama birimine "access_token" ve "expires_in" değerlerini önbelleğe almak için tavsiye edilir. Belirteç veri daha sonra depolama biriminden alınan ve yeniden, Media Services REST API çağrılarında kullanılan. Bu, özellikle burada belirteç güvenli bir şekilde birden çok bilgisayar veya işlemler arasında paylaşılabilir senaryoları için kullanışlıdır.
> 
> 

Erişim belirteci "expires_in" değerini izlemek ve gerektiğinde, REST API çağrıları yeni belirteçleri ile güncelleştirmek emin olun.

### <a name="connecting-to-the-media-services-uri"></a>URI Media Services'e bağlanma
Media Services için URI https://media.windows.net/ köküdür. Bu URI başlangıçta bağlanmanız gerekir ve yanıt olarak 301 yeniden yönlendir alırsanız, yeni bir URI yapılan sonraki çağrılar olmanız gerekir. Ayrıca, herhangi bir yeniden yönlendirme/takip otomatik mantık isteklerinizi kullanmayın. HTTP fiilleri ve istek gövdelerine yeni bir URI iletilen değil.

Depolama hesabı adı ile aynı Media Services hesap kurulumu sırasında kullanılan olduğu varlık dosya yükleme ve indirme için URI kök https://yourstorageaccount.blob.core.windows.net/ olduğuna dikkat edin.

Aşağıdaki örnek, Media Services kök URI (https://media.windows.net/) için HTTP isteği gösterir. İstek 301 yeniden yönlendirme yanıt olarak alır. Sonraki istek yeni bir URI (https://wamsbayclus001rest-hs.cloudapp.net/api/) kullanıyor.     

**HTTP isteği**:

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


**HTTP yanıtı**:

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
    Server: Microsoft-IIS/8.5
    request-id: 987d7652-497a-44e5-b815-f492e02aef97
    x-ms-request-id: 987d7652-497a-44e5-b815-f492e02aef97
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:53 GMT
    Content-Length: 164

    <html><head><title>Object moved</title></head><body>
    <h2>Object moved to <a href="https://wamsbayclus001rest-hs.cloudapp.net/api/">here</a>.</h2>
    </body></html>


**HTTP isteği** (yeni bir URI kullanarak):

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


**HTTP yanıtı**:

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1250
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    x-ms-request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata","value":[{"name":"AccessPolicies","url":"AccessPolicies"},{"name":"Locators","url":"Locators"},{"name":"ContentKeys","url":"ContentKeys"},{"name":"ContentKeyAuthorizationPolicyOptions","url":"ContentKeyAuthorizationPolicyOptions"},{"name":"ContentKeyAuthorizationPolicies","url":"ContentKeyAuthorizationPolicies"},{"name":"Files","url":"Files"},{"name":"Assets","url":"Assets"},{"name":"AssetDeliveryPolicies","url":"AssetDeliveryPolicies"},{"name":"IngestManifestFiles","url":"IngestManifestFiles"},{"name":"IngestManifestAssets","url":"IngestManifestAssets"},{"name":"IngestManifests","url":"IngestManifests"},{"name":"StorageAccounts","url":"StorageAccounts"},{"name":"Tasks","url":"Tasks"},{"name":"NotificationEndPoints","url":"NotificationEndPoints"},{"name":"Jobs","url":"Jobs"},{"name":"TaskTemplates","url":"TaskTemplates"},{"name":"JobTemplates","url":"JobTemplates"},{"name":"MediaProcessors","url":"MediaProcessors"},{"name":"EncodingReservedUnitTypes","url":"EncodingReservedUnitTypes"},{"name":"Operations","url":"Operations"},{"name":"StreamingEndpoints","url":"StreamingEndpoints"},{"name":"Channels","url":"Channels"},{"name":"Programs","url":"Programs"}]}



> [!NOTE]
> Yeni bir URI aldıktan sonra Media Services ile iletişim kurmak için kullanılması gereken URI olmasıdır. 
> 
> 

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

