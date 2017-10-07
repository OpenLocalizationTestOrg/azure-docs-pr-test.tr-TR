---
title: "aaaConnecting tooMedia Hizmetleri REST API kullanarak hesabı | Microsoft Docs"
description: "Bu konuda nasıl tooconnect tooMedia Hizmetleri kullanarak REST gösterilir API."
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
ms.openlocfilehash: 1d5064a3612dc96f5c5ad910d183d84fb70a3b6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-toomedia-services-account-using-media-services-rest-api"></a>TooMedia hizmetleri hesabı Media Services REST API kullanarak bağlanma
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-connect-programmatically.md)
> * [REST](media-services-rest-connect-programmatically.md)
> 
> 

Bu konuda nasıl tooobtain programlı bağlantı tooMicrosoft Azure Media Services ile programlamada hello Media Services REST API açıklanmaktadır.

Microsoft Azure Media Services erişirken iki şey gereklidir: Azure erişim denetimi Hizmetleri (ACS) ve hello Media Services URI tarafından kendisine sağlanan bir erişim belirteci. Merhaba doğru üstbilgi değerlerini belirtin ve Media Services'e çağırırken doğru hello erişim belirtecinde yer geçirin sürece bu istekleri oluştururken, istediğiniz herhangi bir yöntem kullanabilirsiniz.

Merhaba Media Services REST API tooconnect tooMedia kullanarak hizmetleri zaman aşağıdaki adımları hello hello en yaygın iş akışını açıklar:

1. Bir erişim belirteci alma 
2. Medya Hizmetleri URI toohello bağlanma 
   
   > [!NOTE]
   > Başarıyla toohttps://media.windows.net bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız. Sonraki çağrılar toohello yapmanız gereken yeni bir URI.
   > Merhaba ODATA API meta veri açıklamasını içeren bir HTTP/1.1 200 yanıtı de alabilirsiniz.
   > 
   > 
3. Sonraki API çağrıları toohello yeni URL'nizi gönderin. 
   
    Örneğin, tooconnect çalışıyorsanız, sonra hello aşağıdaki var:
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    Sonraki API çağrıları toohttps://wamsbayclus001rest-hs.cloudapp.net/api/ göndermeniz gerekir.

    >[!NOTE]
    >Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için). Merhaba kullanması gereken her zaman kullanıyorsanız, aynı ilke kimliği hello aynı gün / erişim izinlerini, örneğin, uzun bir süre (karşıya yükleme olmayan ilkeleri) yerinde hedeflenen tooremain olan bulucular ilkeleri. Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.

## <a name="access-control-address"></a>Erişim denetimi adresi
Media Services erişim denetimi https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn olduğu Kuzey Çin bölgesi dışında https://wamsprodglobal001acs.accesscontrol.windows.net adresidir.

## <a name="getting-an-access-token"></a>Bir erişim belirteci alma
tooaccess Media Services doğrudan hello REST API aracılığıyla ACS bir erişim belirteci almak ve hello hizmetinde yaptığınız her HTTP isteği sırasında kullanın. Bir HTTP isteği ve hello OAuth v2 protokolünü kullanarak hello üstbilgisinde sağlanan erişim talepler bağlı ACS tarafından sağlanan benzer tooother belirteçleri belirtecidir. Herhangi bir önkoşulu tooMedia Hizmetleri doğrudan bağlanmadan önce gerekmez.

Merhaba aşağıdaki örnek hello HTTP istek üstbilgisi ve kullanılan gövde tooretrieve bir belirteç gösterir.

**Üstbilgi**:

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


**Gövde**:

Bu istek hello gövdesinde tooprove hello client_id ve client_secret değerleri gerekir; client_id ve client_secret toohello AccountName ve AccountKey değerler, sırasıyla karşılık gelir. Hesabınızı ayarladığınızda, bu değerleri tooyou Media Services tarafından sağlanır. 

Media Services hesabınızı URL kodlanmış olmalıdır, hello AccountKey unutmayın (bkz [yüzde kodlama](http://tools.ietf.org/html/rfc3986#section-2.1) erişim belirteci isteğiniz hello client_secret değer olarak kullanırken.

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


Örneğin: 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


Merhaba aşağıdaki örnek hello erişim içeren hello HTTP yanıtı hello yanıt gövdesi içinde belirteci gösterir.

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
> Toocache hello "access_token" ve "expires_in" değerlerini tooan harici depolama önerilir. Merhaba belirteç veri daha sonra hello depolama biriminden alınan ve yeniden, Media Services REST API çağrılarında kullanılan. Bu, özellikle burada hello belirteci güvenli bir şekilde birden çok bilgisayar veya işlemler arasında paylaşılabilir senaryoları için kullanışlıdır.
> 
> 

Emin toomonitor hello "expires_in" değerini hello erişim belirteci yapın ve gerektiği şekilde, REST API çağrıları yeni belirteçleri ile güncelleştirin.

### <a name="connecting-toohello-media-services-uri"></a>Medya Hizmetleri URI toohello bağlanma
Merhaba Media Services için URI https://media.windows.net/ köküdür. Başlangıçta toothis URI bağlanmanız gerekir ve yanıt olarak 301 yeniden yönlendir alırsanız, sonraki çağrılar toohello olmalısınız yeni bir URI. Ayrıca, herhangi bir yeniden yönlendirme/takip otomatik mantık isteklerinizi kullanmayın. HTTP fiilleri ve istek gövdelerine değil iletilir toohello yeni bir URI.

Karşıya yükleme ve varlık dosyaları indirme için URI https://yourstorageaccount.blob.core.windows.net/ hello depolama hesabı adı hello Media Services hesap kurulumu sırasında kullanılan aynı olduğu bu hello kök unutmayın.

Aşağıdaki örnek hello HTTP isteği toohello Media Services kök URI (https://media.windows.net/) gösterir. Merhaba istek 301 yeniden yönlendirme yanıt olarak alır. Merhaba Taleplerde kullanan yeni bir URI (https://wamsbayclus001rest-hs.cloudapp.net/api/) hello.     

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
    <h2>Object moved too<a href="https://wamsbayclus001rest-hs.cloudapp.net/api/">here</a>.</h2>
    </body></html>


**HTTP isteği** (yeni bir URI hello kullanarak):

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
> Merhaba yeni aldıktan sonra URI, Media Services ile kullanılan toocommunicate olmalıdır URI hello. 
> 
> 

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

