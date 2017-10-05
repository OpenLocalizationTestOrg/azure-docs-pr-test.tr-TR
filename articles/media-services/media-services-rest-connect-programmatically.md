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
# <a name="connecting-to-media-services-account-using-media-services-rest-api"></a><span data-ttu-id="c1a5b-103">Media Services REST API kullanarak Media Services hesabına bağlanma</span><span class="sxs-lookup"><span data-stu-id="c1a5b-103">Connecting to Media Services Account using Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c1a5b-104">.NET</span><span class="sxs-lookup"><span data-stu-id="c1a5b-104">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> * [<span data-ttu-id="c1a5b-105">REST</span><span class="sxs-lookup"><span data-stu-id="c1a5b-105">REST</span></span>](media-services-rest-connect-programmatically.md)
> 
> 

<span data-ttu-id="c1a5b-106">Bu konu, Media Services REST API ile programlama yaparken Microsoft Azure Media Services programlama bağlantı elde açıklar.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-106">This topic describes how to obtain a programmatic connection to Microsoft Azure Media Services when you are programming with the Media Services REST API.</span></span>

<span data-ttu-id="c1a5b-107">Microsoft Azure Media Services erişirken iki şey gereklidir: Azure erişim denetimi Hizmetleri (ACS) ve Media Services URI tarafından kendisine sağlanan bir erişim belirteci.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-107">Two things are required when accessing Microsoft Azure Media Services: An access token provided by Azure Access Control Services (ACS), and the URI of Media Services itself.</span></span> <span data-ttu-id="c1a5b-108">Bu istekler doğru üstbilgi değerlerini belirtin ve Media Services'e çağırırken doğru erişim belirtecinde yer geçirin sürece oluştururken, istediğiniz herhangi bir yöntem kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-108">You can use any means you want when creating these requests as long as you specify the correct header values and pass in the access token correctly when calling into Media Services.</span></span>

<span data-ttu-id="c1a5b-109">Aşağıdaki adımlar, Media Services'e bağlanmak için Media Services REST API kullanırken en yaygın iş akışını açıklar:</span><span class="sxs-lookup"><span data-stu-id="c1a5b-109">The following steps describe the most common workflow when using the Media Services REST API to connect to Media Services:</span></span>

1. <span data-ttu-id="c1a5b-110">Bir erişim belirteci alma</span><span class="sxs-lookup"><span data-stu-id="c1a5b-110">Getting an access token</span></span> 
2. <span data-ttu-id="c1a5b-111">URI Media Services'e bağlanma</span><span class="sxs-lookup"><span data-stu-id="c1a5b-111">Connecting to the Media Services URI</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="c1a5b-112">Başarıyla https://media.windows.net için bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-112">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="c1a5b-113">Yeni bir URI yapılan sonraki çağrılar yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-113">You must make subsequent calls to the new URI.</span></span>
   > <span data-ttu-id="c1a5b-114">ODATA API meta veri açıklamasını içeren bir HTTP/1.1 200 yanıtı de alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-114">You may also receive a HTTP/1.1 200 response that contains the ODATA API metadata description.</span></span>
   > 
   > 
3. <span data-ttu-id="c1a5b-115">Yeni URL, sonraki API çağrıları gönderin.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-115">Post your subsequent API calls to the new URL.</span></span> 
   
    <span data-ttu-id="c1a5b-116">Örneğin, bağlanmaya varsa sonra aşağıdaki aldığınız:</span><span class="sxs-lookup"><span data-stu-id="c1a5b-116">For example, if after trying to connect, you got the following:</span></span>
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    <span data-ttu-id="c1a5b-117">Sonraki API aramalarınız https://wamsbayclus001rest-hs.cloudapp.net/api/ göndermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-117">You should post your subsequent API calls to https://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

    >[!NOTE]
    ><span data-ttu-id="c1a5b-118">Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için).</span><span class="sxs-lookup"><span data-stu-id="c1a5b-118">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="c1a5b-119">Uzun süre boyunca kullanılmak için oluşturulan bulucu ilkeleri gibi aynı günleri / erişim izinlerini sürekli olarak kullanıyorsanız, aynı ilke kimliğini kullanmalısınız (karşıya yükleme olmayan ilkeler için).</span><span class="sxs-lookup"><span data-stu-id="c1a5b-119">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="c1a5b-120">Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-120">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="access-control-address"></a><span data-ttu-id="c1a5b-121">Erişim denetimi adresi</span><span class="sxs-lookup"><span data-stu-id="c1a5b-121">Access control address</span></span>
<span data-ttu-id="c1a5b-122">Media Services erişim denetimi https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn olduğu Kuzey Çin bölgesi dışında https://wamsprodglobal001acs.accesscontrol.windows.net adresidir.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-122">Media Services access control address is https://wamsprodglobal001acs.accesscontrol.windows.net, except for North China region, where it is https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span></span>

## <a name="getting-an-access-token"></a><span data-ttu-id="c1a5b-123">Bir erişim belirteci alma</span><span class="sxs-lookup"><span data-stu-id="c1a5b-123">Getting an access token</span></span>
<span data-ttu-id="c1a5b-124">Media Services REST API aracılığıyla doğrudan erişmek için ACS bir erişim belirteci almak ve hizmete yaptığınız her HTTP isteği sırasında kullanın.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-124">To access Media Services directly through the REST API, retrieve an access token from ACS and use it during every HTTP request you make into the service.</span></span> <span data-ttu-id="c1a5b-125">Bu belirteç, bir HTTP isteği ve OAuth v2 protokolünü kullanarak üstbilgisinde sağlanan erişim talepler bağlı ACS tarafından sağlanan diğer belirteçleri benzerdir.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-125">This token is similar to other tokens provided by ACS based on access claims provided in the header of an HTTP request and using the OAuth v2 protocol.</span></span> <span data-ttu-id="c1a5b-126">Herhangi bir önkoşulu Media Services'e doğrudan bağlanmadan önce gerekmez.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-126">You do not need any other prerequisites before directly connecting to Media Services.</span></span>

<span data-ttu-id="c1a5b-127">Aşağıdaki örnek HTTP istek üstbilgisi ve bir belirteç almak için kullanılan gövde gösterir.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-127">The following example shows the HTTP request header and body used to retrieve a token.</span></span>

<span data-ttu-id="c1a5b-128">**Üstbilgi**:</span><span class="sxs-lookup"><span data-stu-id="c1a5b-128">**Header**:</span></span>

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


<span data-ttu-id="c1a5b-129">**Gövde**:</span><span class="sxs-lookup"><span data-stu-id="c1a5b-129">**Body**:</span></span>

<span data-ttu-id="c1a5b-130">Bu istek gövdesinde client_id ve client_secret değerleri kanıtlamanız gerekir; AccountName ve AccountKey değerleri için sırasıyla client_id ve client_secret karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-130">You need to prove the client_id and client_secret values in the body of this request; client_id and client_secret correspond to the AccountName and AccountKey values, respectively.</span></span> <span data-ttu-id="c1a5b-131">Hesabınızı ayarladığınızda, bu değerler, Media Services tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-131">These values are provided to you by Media Services when you set up your account.</span></span> 

<span data-ttu-id="c1a5b-132">Media Services hesabınızı AccountKey URL kodlanmış olması gerektiğini unutmayın (bkz [yüzde kodlama](http://tools.ietf.org/html/rfc3986#section-2.1) erişim belirteci isteğiniz client_secret değer olarak kullanırken.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-132">Note that the AccountKey for your Media Services account must be URL-encoded (see [Percent-Encoding](http://tools.ietf.org/html/rfc3986#section-2.1) when using it as the client_secret value in your access token request.</span></span>

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="c1a5b-133">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="c1a5b-133">For example:</span></span> 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="c1a5b-134">Aşağıdaki örnek erişimi içeren HTTP yanıtı yanıt gövdesinde belirteci gösterir.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-134">The following example shows the HTTP response that contains the access token in the response body.</span></span>

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
> <span data-ttu-id="c1a5b-135">Bir dış depolama birimine "access_token" ve "expires_in" değerlerini önbelleğe almak için tavsiye edilir.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-135">It is recommended to cache the "access_token " and "expires_in " values to an external storage.</span></span> <span data-ttu-id="c1a5b-136">Belirteç veri daha sonra depolama biriminden alınan ve yeniden, Media Services REST API çağrılarında kullanılan.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-136">The token data could later be retrieved from the storage and re-used in your Media Services REST API calls.</span></span> <span data-ttu-id="c1a5b-137">Bu, özellikle burada belirteç güvenli bir şekilde birden çok bilgisayar veya işlemler arasında paylaşılabilir senaryoları için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-137">This is especially useful for scenarios where the token can be securely shared among multiple processes or computers.</span></span>
> 
> 

<span data-ttu-id="c1a5b-138">Erişim belirteci "expires_in" değerini izlemek ve gerektiğinde, REST API çağrıları yeni belirteçleri ile güncelleştirmek emin olun.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-138">Make sure to monitor the "expires_in" value of the access token and update your REST API calls with new tokens as needed.</span></span>

### <a name="connecting-to-the-media-services-uri"></a><span data-ttu-id="c1a5b-139">URI Media Services'e bağlanma</span><span class="sxs-lookup"><span data-stu-id="c1a5b-139">Connecting to the Media Services URI</span></span>
<span data-ttu-id="c1a5b-140">Media Services için URI https://media.windows.net/ köküdür.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-140">The root URI for Media Services is https://media.windows.net/.</span></span> <span data-ttu-id="c1a5b-141">Bu URI başlangıçta bağlanmanız gerekir ve yanıt olarak 301 yeniden yönlendir alırsanız, yeni bir URI yapılan sonraki çağrılar olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-141">You should initially connect to this URI, and if you get a 301 redirect back in response, you should make subsequent calls to the new URI.</span></span> <span data-ttu-id="c1a5b-142">Ayrıca, herhangi bir yeniden yönlendirme/takip otomatik mantık isteklerinizi kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-142">In addition, do not use any auto-redirect/follow logic in your requests.</span></span> <span data-ttu-id="c1a5b-143">HTTP fiilleri ve istek gövdelerine yeni bir URI iletilen değil.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-143">HTTP verbs and request bodies will not be forwarded to the new URI.</span></span>

<span data-ttu-id="c1a5b-144">Depolama hesabı adı ile aynı Media Services hesap kurulumu sırasında kullanılan olduğu varlık dosya yükleme ve indirme için URI kök https://yourstorageaccount.blob.core.windows.net/ olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-144">Note that the root URI for uploading and downloading Asset files is https://yourstorageaccount.blob.core.windows.net/ where the storage account name is the same one you used during your Media Services account setup.</span></span>

<span data-ttu-id="c1a5b-145">Aşağıdaki örnek, Media Services kök URI (https://media.windows.net/) için HTTP isteği gösterir.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-145">The following example demonstrates HTTP request to the Media Services root URI (https://media.windows.net/).</span></span> <span data-ttu-id="c1a5b-146">İstek 301 yeniden yönlendirme yanıt olarak alır.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-146">The request gets a 301 redirect back in response.</span></span> <span data-ttu-id="c1a5b-147">Sonraki istek yeni bir URI (https://wamsbayclus001rest-hs.cloudapp.net/api/) kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-147">The subsequent request is using the new URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span></span>     

<span data-ttu-id="c1a5b-148">**HTTP isteği**:</span><span class="sxs-lookup"><span data-stu-id="c1a5b-148">**HTTP Request**:</span></span>

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


<span data-ttu-id="c1a5b-149">**HTTP yanıtı**:</span><span class="sxs-lookup"><span data-stu-id="c1a5b-149">**HTTP Response**:</span></span>

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


<span data-ttu-id="c1a5b-150">**HTTP isteği** (yeni bir URI kullanarak):</span><span class="sxs-lookup"><span data-stu-id="c1a5b-150">**HTTP Request** (using the new URI):</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="c1a5b-151">**HTTP yanıtı**:</span><span class="sxs-lookup"><span data-stu-id="c1a5b-151">**HTTP Response**:</span></span>

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
> <span data-ttu-id="c1a5b-152">Yeni bir URI aldıktan sonra Media Services ile iletişim kurmak için kullanılması gereken URI olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="c1a5b-152">Once you get the new URI, that is the URI that should be used to communicate with Media Services.</span></span> 
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="c1a5b-153">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="c1a5b-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c1a5b-154">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="c1a5b-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

