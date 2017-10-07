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
# <a name="connecting-toomedia-services-account-using-media-services-rest-api"></a><span data-ttu-id="af947-103">TooMedia hizmetleri hesabı Media Services REST API kullanarak bağlanma</span><span class="sxs-lookup"><span data-stu-id="af947-103">Connecting tooMedia Services Account using Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="af947-104">.NET</span><span class="sxs-lookup"><span data-stu-id="af947-104">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> * [<span data-ttu-id="af947-105">REST</span><span class="sxs-lookup"><span data-stu-id="af947-105">REST</span></span>](media-services-rest-connect-programmatically.md)
> 
> 

<span data-ttu-id="af947-106">Bu konuda nasıl tooobtain programlı bağlantı tooMicrosoft Azure Media Services ile programlamada hello Media Services REST API açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="af947-106">This topic describes how tooobtain a programmatic connection tooMicrosoft Azure Media Services when you are programming with hello Media Services REST API.</span></span>

<span data-ttu-id="af947-107">Microsoft Azure Media Services erişirken iki şey gereklidir: Azure erişim denetimi Hizmetleri (ACS) ve hello Media Services URI tarafından kendisine sağlanan bir erişim belirteci.</span><span class="sxs-lookup"><span data-stu-id="af947-107">Two things are required when accessing Microsoft Azure Media Services: An access token provided by Azure Access Control Services (ACS), and hello URI of Media Services itself.</span></span> <span data-ttu-id="af947-108">Merhaba doğru üstbilgi değerlerini belirtin ve Media Services'e çağırırken doğru hello erişim belirtecinde yer geçirin sürece bu istekleri oluştururken, istediğiniz herhangi bir yöntem kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af947-108">You can use any means you want when creating these requests as long as you specify hello correct header values and pass in hello access token correctly when calling into Media Services.</span></span>

<span data-ttu-id="af947-109">Merhaba Media Services REST API tooconnect tooMedia kullanarak hizmetleri zaman aşağıdaki adımları hello hello en yaygın iş akışını açıklar:</span><span class="sxs-lookup"><span data-stu-id="af947-109">hello following steps describe hello most common workflow when using hello Media Services REST API tooconnect tooMedia Services:</span></span>

1. <span data-ttu-id="af947-110">Bir erişim belirteci alma</span><span class="sxs-lookup"><span data-stu-id="af947-110">Getting an access token</span></span> 
2. <span data-ttu-id="af947-111">Medya Hizmetleri URI toohello bağlanma</span><span class="sxs-lookup"><span data-stu-id="af947-111">Connecting toohello Media Services URI</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="af947-112">Başarıyla toohttps://media.windows.net bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız.</span><span class="sxs-lookup"><span data-stu-id="af947-112">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="af947-113">Sonraki çağrılar toohello yapmanız gereken yeni bir URI.</span><span class="sxs-lookup"><span data-stu-id="af947-113">You must make subsequent calls toohello new URI.</span></span>
   > <span data-ttu-id="af947-114">Merhaba ODATA API meta veri açıklamasını içeren bir HTTP/1.1 200 yanıtı de alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af947-114">You may also receive a HTTP/1.1 200 response that contains hello ODATA API metadata description.</span></span>
   > 
   > 
3. <span data-ttu-id="af947-115">Sonraki API çağrıları toohello yeni URL'nizi gönderin.</span><span class="sxs-lookup"><span data-stu-id="af947-115">Post your subsequent API calls toohello new URL.</span></span> 
   
    <span data-ttu-id="af947-116">Örneğin, tooconnect çalışıyorsanız, sonra hello aşağıdaki var:</span><span class="sxs-lookup"><span data-stu-id="af947-116">For example, if after trying tooconnect, you got hello following:</span></span>
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    <span data-ttu-id="af947-117">Sonraki API çağrıları toohttps://wamsbayclus001rest-hs.cloudapp.net/api/ göndermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="af947-117">You should post your subsequent API calls toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

    >[!NOTE]
    ><span data-ttu-id="af947-118">Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için).</span><span class="sxs-lookup"><span data-stu-id="af947-118">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="af947-119">Merhaba kullanması gereken her zaman kullanıyorsanız, aynı ilke kimliği hello aynı gün / erişim izinlerini, örneğin, uzun bir süre (karşıya yükleme olmayan ilkeleri) yerinde hedeflenen tooremain olan bulucular ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="af947-119">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="af947-120">Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="af947-120">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="access-control-address"></a><span data-ttu-id="af947-121">Erişim denetimi adresi</span><span class="sxs-lookup"><span data-stu-id="af947-121">Access control address</span></span>
<span data-ttu-id="af947-122">Media Services erişim denetimi https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn olduğu Kuzey Çin bölgesi dışında https://wamsprodglobal001acs.accesscontrol.windows.net adresidir.</span><span class="sxs-lookup"><span data-stu-id="af947-122">Media Services access control address is https://wamsprodglobal001acs.accesscontrol.windows.net, except for North China region, where it is https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span></span>

## <a name="getting-an-access-token"></a><span data-ttu-id="af947-123">Bir erişim belirteci alma</span><span class="sxs-lookup"><span data-stu-id="af947-123">Getting an access token</span></span>
<span data-ttu-id="af947-124">tooaccess Media Services doğrudan hello REST API aracılığıyla ACS bir erişim belirteci almak ve hello hizmetinde yaptığınız her HTTP isteği sırasında kullanın.</span><span class="sxs-lookup"><span data-stu-id="af947-124">tooaccess Media Services directly through hello REST API, retrieve an access token from ACS and use it during every HTTP request you make into hello service.</span></span> <span data-ttu-id="af947-125">Bir HTTP isteği ve hello OAuth v2 protokolünü kullanarak hello üstbilgisinde sağlanan erişim talepler bağlı ACS tarafından sağlanan benzer tooother belirteçleri belirtecidir.</span><span class="sxs-lookup"><span data-stu-id="af947-125">This token is similar tooother tokens provided by ACS based on access claims provided in hello header of an HTTP request and using hello OAuth v2 protocol.</span></span> <span data-ttu-id="af947-126">Herhangi bir önkoşulu tooMedia Hizmetleri doğrudan bağlanmadan önce gerekmez.</span><span class="sxs-lookup"><span data-stu-id="af947-126">You do not need any other prerequisites before directly connecting tooMedia Services.</span></span>

<span data-ttu-id="af947-127">Merhaba aşağıdaki örnek hello HTTP istek üstbilgisi ve kullanılan gövde tooretrieve bir belirteç gösterir.</span><span class="sxs-lookup"><span data-stu-id="af947-127">hello following example shows hello HTTP request header and body used tooretrieve a token.</span></span>

<span data-ttu-id="af947-128">**Üstbilgi**:</span><span class="sxs-lookup"><span data-stu-id="af947-128">**Header**:</span></span>

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


<span data-ttu-id="af947-129">**Gövde**:</span><span class="sxs-lookup"><span data-stu-id="af947-129">**Body**:</span></span>

<span data-ttu-id="af947-130">Bu istek hello gövdesinde tooprove hello client_id ve client_secret değerleri gerekir; client_id ve client_secret toohello AccountName ve AccountKey değerler, sırasıyla karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="af947-130">You need tooprove hello client_id and client_secret values in hello body of this request; client_id and client_secret correspond toohello AccountName and AccountKey values, respectively.</span></span> <span data-ttu-id="af947-131">Hesabınızı ayarladığınızda, bu değerleri tooyou Media Services tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="af947-131">These values are provided tooyou by Media Services when you set up your account.</span></span> 

<span data-ttu-id="af947-132">Media Services hesabınızı URL kodlanmış olmalıdır, hello AccountKey unutmayın (bkz [yüzde kodlama](http://tools.ietf.org/html/rfc3986#section-2.1) erişim belirteci isteğiniz hello client_secret değer olarak kullanırken.</span><span class="sxs-lookup"><span data-stu-id="af947-132">Note that hello AccountKey for your Media Services account must be URL-encoded (see [Percent-Encoding](http://tools.ietf.org/html/rfc3986#section-2.1) when using it as hello client_secret value in your access token request.</span></span>

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="af947-133">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="af947-133">For example:</span></span> 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="af947-134">Merhaba aşağıdaki örnek hello erişim içeren hello HTTP yanıtı hello yanıt gövdesi içinde belirteci gösterir.</span><span class="sxs-lookup"><span data-stu-id="af947-134">hello following example shows hello HTTP response that contains hello access token in hello response body.</span></span>

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
> <span data-ttu-id="af947-135">Toocache hello "access_token" ve "expires_in" değerlerini tooan harici depolama önerilir.</span><span class="sxs-lookup"><span data-stu-id="af947-135">It is recommended toocache hello "access_token " and "expires_in " values tooan external storage.</span></span> <span data-ttu-id="af947-136">Merhaba belirteç veri daha sonra hello depolama biriminden alınan ve yeniden, Media Services REST API çağrılarında kullanılan.</span><span class="sxs-lookup"><span data-stu-id="af947-136">hello token data could later be retrieved from hello storage and re-used in your Media Services REST API calls.</span></span> <span data-ttu-id="af947-137">Bu, özellikle burada hello belirteci güvenli bir şekilde birden çok bilgisayar veya işlemler arasında paylaşılabilir senaryoları için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="af947-137">This is especially useful for scenarios where hello token can be securely shared among multiple processes or computers.</span></span>
> 
> 

<span data-ttu-id="af947-138">Emin toomonitor hello "expires_in" değerini hello erişim belirteci yapın ve gerektiği şekilde, REST API çağrıları yeni belirteçleri ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="af947-138">Make sure toomonitor hello "expires_in" value of hello access token and update your REST API calls with new tokens as needed.</span></span>

### <a name="connecting-toohello-media-services-uri"></a><span data-ttu-id="af947-139">Medya Hizmetleri URI toohello bağlanma</span><span class="sxs-lookup"><span data-stu-id="af947-139">Connecting toohello Media Services URI</span></span>
<span data-ttu-id="af947-140">Merhaba Media Services için URI https://media.windows.net/ köküdür.</span><span class="sxs-lookup"><span data-stu-id="af947-140">hello root URI for Media Services is https://media.windows.net/.</span></span> <span data-ttu-id="af947-141">Başlangıçta toothis URI bağlanmanız gerekir ve yanıt olarak 301 yeniden yönlendir alırsanız, sonraki çağrılar toohello olmalısınız yeni bir URI.</span><span class="sxs-lookup"><span data-stu-id="af947-141">You should initially connect toothis URI, and if you get a 301 redirect back in response, you should make subsequent calls toohello new URI.</span></span> <span data-ttu-id="af947-142">Ayrıca, herhangi bir yeniden yönlendirme/takip otomatik mantık isteklerinizi kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="af947-142">In addition, do not use any auto-redirect/follow logic in your requests.</span></span> <span data-ttu-id="af947-143">HTTP fiilleri ve istek gövdelerine değil iletilir toohello yeni bir URI.</span><span class="sxs-lookup"><span data-stu-id="af947-143">HTTP verbs and request bodies will not be forwarded toohello new URI.</span></span>

<span data-ttu-id="af947-144">Karşıya yükleme ve varlık dosyaları indirme için URI https://yourstorageaccount.blob.core.windows.net/ hello depolama hesabı adı hello Media Services hesap kurulumu sırasında kullanılan aynı olduğu bu hello kök unutmayın.</span><span class="sxs-lookup"><span data-stu-id="af947-144">Note that hello root URI for uploading and downloading Asset files is https://yourstorageaccount.blob.core.windows.net/ where hello storage account name is hello same one you used during your Media Services account setup.</span></span>

<span data-ttu-id="af947-145">Aşağıdaki örnek hello HTTP isteği toohello Media Services kök URI (https://media.windows.net/) gösterir.</span><span class="sxs-lookup"><span data-stu-id="af947-145">hello following example demonstrates HTTP request toohello Media Services root URI (https://media.windows.net/).</span></span> <span data-ttu-id="af947-146">Merhaba istek 301 yeniden yönlendirme yanıt olarak alır.</span><span class="sxs-lookup"><span data-stu-id="af947-146">hello request gets a 301 redirect back in response.</span></span> <span data-ttu-id="af947-147">Merhaba Taleplerde kullanan yeni bir URI (https://wamsbayclus001rest-hs.cloudapp.net/api/) hello.</span><span class="sxs-lookup"><span data-stu-id="af947-147">hello subsequent request is using hello new URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span></span>     

<span data-ttu-id="af947-148">**HTTP isteği**:</span><span class="sxs-lookup"><span data-stu-id="af947-148">**HTTP Request**:</span></span>

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


<span data-ttu-id="af947-149">**HTTP yanıtı**:</span><span class="sxs-lookup"><span data-stu-id="af947-149">**HTTP Response**:</span></span>

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


<span data-ttu-id="af947-150">**HTTP isteği** (yeni bir URI hello kullanarak):</span><span class="sxs-lookup"><span data-stu-id="af947-150">**HTTP Request** (using hello new URI):</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="af947-151">**HTTP yanıtı**:</span><span class="sxs-lookup"><span data-stu-id="af947-151">**HTTP Response**:</span></span>

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
> <span data-ttu-id="af947-152">Merhaba yeni aldıktan sonra URI, Media Services ile kullanılan toocommunicate olmalıdır URI hello.</span><span class="sxs-lookup"><span data-stu-id="af947-152">Once you get hello new URI, that is hello URI that should be used toocommunicate with Media Services.</span></span> 
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="af947-153">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="af947-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="af947-154">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="af947-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

