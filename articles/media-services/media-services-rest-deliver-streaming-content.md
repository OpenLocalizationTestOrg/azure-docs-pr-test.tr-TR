---
title: "REST kullanarak aaaPublish Azure Media Services içerik"
description: "Bilgi nasıl toocreate kullanılan toobuild bir akış URL'si olan bir Bulucu. Merhaba kod REST API'sini kullanır."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: ff332c30-30c6-4ed1-99d0-5fffd25d4f23
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: f849e21b3103b9b33bc652e886b2016ea495b19a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-azure-media-services-content-using-rest"></a><span data-ttu-id="d3830-104">REST kullanarak Azure Media Services içerik yayımlama</span><span class="sxs-lookup"><span data-stu-id="d3830-104">Publish Azure Media Services content using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d3830-105">.NET</span><span class="sxs-lookup"><span data-stu-id="d3830-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="d3830-106">REST</span><span class="sxs-lookup"><span data-stu-id="d3830-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> * [<span data-ttu-id="d3830-107">Portal</span><span class="sxs-lookup"><span data-stu-id="d3830-107">Portal</span></span>](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="d3830-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="d3830-108">Overview</span></span>
<span data-ttu-id="d3830-109">Bir OnDemand akış Bulucusu oluşturma ve akış URL'si oluşturma MP4 kümesine bir bit hızı Uyarlamalı akışını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3830-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="d3830-110">Merhaba [bir varlık kodlama](media-services-rest-encode-asset.md) konu, bir bit hızı Uyarlamalı MP4 içine tooencode nasıl ayarlanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="d3830-110">hello [encoding an asset](media-services-rest-encode-asset.md) topic shows how tooencode into an adaptive bitrate MP4 set.</span></span> <span data-ttu-id="d3830-111">İçeriğinizi şifrelenmişse, varlık teslim ilkesini yapılandırın (açıklandığı gibi [bu](media-services-rest-configure-asset-delivery-policy.md) konu) bir Bulucu oluşturmadan önce.</span><span class="sxs-lookup"><span data-stu-id="d3830-111">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-rest-configure-asset-delivery-policy.md) topic) before creating a locator.</span></span> 

<span data-ttu-id="d3830-112">Bir OnDemand Bulucu toobuild URL'leri aşamalı olarak indirilebilir bu noktası tooMP4 dosyaları akış de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3830-112">You can also use an OnDemand streaming locator toobuild URLs that point tooMP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="d3830-113">Bu konu, nasıl toocreate bir OnDemand akış Bulucusu Varlığınızı toopublish sipariş ve kesintisiz, MPEG DASH ve akış URL'lerini HLS yapı gösterir.</span><span class="sxs-lookup"><span data-stu-id="d3830-113">This topic shows how toocreate an OnDemand streaming locator in order toopublish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="d3830-114">Ayrıca Dinamik toobuild aşamalı indirme URL'leri gösterir.</span><span class="sxs-lookup"><span data-stu-id="d3830-114">It also shows hot toobuild progressive download URLs.</span></span>

<span data-ttu-id="d3830-115">Merhaba [aşağıdaki](#types) bölüm değerleri kullanılan enum türleri hello hello REST çağrılarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="d3830-115">hello [following](#types) section shows hello enum types whose values are used in hello REST calls.</span></span>   

> [!NOTE]
> <span data-ttu-id="d3830-116">Varlıklar Media Services erişirken, HTTP istekleri özel üstbilgi alanlarını ve değerlerini ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3830-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="d3830-117">Daha fazla bilgi için bkz: [Media Services REST API geliştirme için Kurulum](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="d3830-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-toomedia-services"></a><span data-ttu-id="d3830-118">TooMedia Hizmetleri'ne Bağlama</span><span class="sxs-lookup"><span data-stu-id="d3830-118">Connect tooMedia Services</span></span>

<span data-ttu-id="d3830-119">Nasıl tooconnect toohello AMS API, bkz. bilgi [Azure AD kimlik doğrulaması ile erişim hello Azure Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="d3830-119">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="d3830-120">Başarıyla toohttps://media.windows.net bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız.</span><span class="sxs-lookup"><span data-stu-id="d3830-120">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="d3830-121">Sonraki çağrılar toohello yapmanız gereken yeni bir URI.</span><span class="sxs-lookup"><span data-stu-id="d3830-121">You must make subsequent calls toohello new URI.</span></span>

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="d3830-122">Bir OnDemand akış Bulucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="d3830-122">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="d3830-123">toocreate OnDemand Bulucu akış hello ve aşağıdaki toodo hello gereken URL'leri alın:</span><span class="sxs-lookup"><span data-stu-id="d3830-123">toocreate hello OnDemand streaming locator and get URLs you need toodo hello following:</span></span>

1. <span data-ttu-id="d3830-124">Merhaba içerik şifrelenmişse, bir erişim ilkesi tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="d3830-124">If hello content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="d3830-125">Bir OnDemand Bulucu akış oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d3830-125">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="d3830-126">Toostream planlıyorsanız, hello varlık bildirim dosyasında (.ism) akış hello alın.</span><span class="sxs-lookup"><span data-stu-id="d3830-126">If you plan toostream, get hello streaming manifest file (.ism) in hello asset.</span></span> 
   
   <span data-ttu-id="d3830-127">Tooprogressively indirme planlıyorsanız, hello varlık MP4 dosyaları hello adlarını alır.</span><span class="sxs-lookup"><span data-stu-id="d3830-127">If you plan tooprogressively download, get hello names of MP4 files in hello asset.</span></span> 
4. <span data-ttu-id="d3830-128">URL'leri toohello bildirim dosyası veya MP4 dosyaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d3830-128">Build URLs toohello manifest file or MP4 files.</span></span> 
5. <span data-ttu-id="d3830-129">İçeren bir AccessPolicy kullanarak akış Bulucusu oluşturulamıyor Not yazabilir veya izinleri silin.</span><span class="sxs-lookup"><span data-stu-id="d3830-129">Note that you cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.</span></span>

### <a name="create-an-access-policy"></a><span data-ttu-id="d3830-130">Erişim ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d3830-130">Create an access policy</span></span>

>[!NOTE]
><span data-ttu-id="d3830-131">Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için).</span><span class="sxs-lookup"><span data-stu-id="d3830-131">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="d3830-132">Merhaba kullanması gereken her zaman kullanıyorsanız, aynı ilke kimliği hello aynı gün / erişim izinlerini, örneğin, uzun bir süre (karşıya yükleme olmayan ilkeleri) yerinde hedeflenen tooremain olan bulucular ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="d3830-132">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="d3830-133">Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="d3830-133">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="d3830-134">İsteği:</span><span class="sxs-lookup"><span data-stu-id="d3830-134">Request:</span></span>

    POST https://media.windows.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstest1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1424263184&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=NWE%2f986Hr5lZTzVGKtC%2ftzHm9n6U%2fxpTFULItxKUGC4%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 6bcfd511-a561-448d-a022-a319a89ecffa
    Host: media.windows.net
    Content-Length: 68

    {"Name":"access policy","DurationInMinutes":43200.0,"Permissions":1}

<span data-ttu-id="d3830-135">Yanıtı:</span><span class="sxs-lookup"><span data-stu-id="d3830-135">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 311
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https:/media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3A69c80d98-7830-407f-a9af-e25f4b0d3e5f')
    Server: Microsoft-IIS/8.5
    request-id: a877528a-bdb4-4414-9862-273f8e64f882
    x-ms-request-id: a877528a-bdb4-4414-9862-273f8e64f882
    x-ms-client-request-id: 6bcfd511-a561-448d-a022-a319a89ecffa
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 18 Feb 2015 06:52:09 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#AccessPolicies/@Element","Id":"nb:pid:UUID:69c80d98-7830-407f-a9af-e25f4b0d3e5f","Created":"2015-02-18T06:52:09.8862191Z","LastModified":"2015-02-18T06:52:09.8862191Z","Name":"access policy","DurationInMinutes":43200.0,"Permissions":1}

### <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="d3830-136">Bir OnDemand akış Bulucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="d3830-136">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="d3830-137">Merhaba belirtilen varlık ve varlık ilkesini Hello Bulucu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d3830-137">Create hello locator for hello specified asset and asset policy.</span></span>

<span data-ttu-id="d3830-138">İsteği:</span><span class="sxs-lookup"><span data-stu-id="d3830-138">Request:</span></span>

    POST https://media.windows.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstest1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1424263184&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=NWE%2f986Hr5lZTzVGKtC%2ftzHm9n6U%2fxpTFULItxKUGC4%3d
    x-ms-version: 2.11
    x-ms-client-request-id: ac159492-9a0c-40c3-aacc-551b1b4c5f62
    Host: media.windows.net
    Content-Length: 181

    {"AccessPolicyId":"nb:pid:UUID:1480030d-c481-430a-9687-535c6a5cb272","AssetId":"nb:cid:UUID:cc1e445d-1500-80bd-538e-f1e4b71b465e","StartTime":"2015-02-18T06:34:47.267872Z","Type":2}

<span data-ttu-id="d3830-139">Yanıtı:</span><span class="sxs-lookup"><span data-stu-id="d3830-139">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 637
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Abe245661-2bbd-4fc6-b14f-9cf9a1492e5e')
    Server: Microsoft-IIS/8.5
    request-id: 5bd5864a-0afd-44c0-a67a-4044a2c9043b
    x-ms-request-id: 5bd5864a-0afd-44c0-a67a-4044a2c9043b
    x-ms-client-request-id: ac159492-9a0c-40c3-aacc-551b1b4c5f62
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 18 Feb 2015 06:58:37 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#Locators/@Element","Id":"nb:lid:UUID:be245661-2bbd-4fc6-b14f-9cf9a1492e5e","ExpirationDateTime":"2015-03-20T06:34:47.267872+00:00","Type":2,"Path":"http://amstest1.streaming.mediaservices.windows.net/be245661-2bbd-4fc6-b14f-9cf9a1492e5e/","BaseUri":"http://amstest1.streaming.mediaservices.windows.net","ContentAccessComponent":"be245661-2bbd-4fc6-b14f-9cf9a1492e5e","AccessPolicyId":"nb:pid:UUID:1480030d-c481-430a-9687-535c6a5cb272","AssetId":"nb:cid:UUID:cc1e445d-1500-80bd-538e-f1e4b71b465e","StartTime":"2015-02-18T06:34:47.267872+00:00","Name":null}

### <a name="build-streaming-urls"></a><span data-ttu-id="d3830-140">Akış URL'lerini derleme</span><span class="sxs-lookup"><span data-stu-id="d3830-140">Build streaming URLs</span></span>
<span data-ttu-id="d3830-141">Kullanım hello **yolu** kesintisiz, HLS ve MPEG DASH URL'leri hello Bulucu toobuild hello hello oluşturulduktan sonra döndürülen değer.</span><span class="sxs-lookup"><span data-stu-id="d3830-141">Use hello **Path** value returned after hello creation of hello locator toobuild hello Smooth, HLS, and MPEG DASH URLs.</span></span> 

<span data-ttu-id="d3830-142">Kesintisiz akış: **yolu** + yayılma dosyası adı + "/ bildirimi"</span><span class="sxs-lookup"><span data-stu-id="d3830-142">Smooth Streaming: **Path** + manifest file name + "/manifest"</span></span>

<span data-ttu-id="d3830-143">Örnek:</span><span class="sxs-lookup"><span data-stu-id="d3830-143">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest

<span data-ttu-id="d3830-144">HLS: **yolu** + yayılma dosyası adı + "/ manifest(format=m3u8-aapl)"</span><span class="sxs-lookup"><span data-stu-id="d3830-144">HLS: **Path** + manifest file name + "/manifest(format=m3u8-aapl)"</span></span>

<span data-ttu-id="d3830-145">Örnek:</span><span class="sxs-lookup"><span data-stu-id="d3830-145">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)


<span data-ttu-id="d3830-146">TİRE: **yolu** + yayılma dosyası adı + "/ manifest(format=mpd-time-csf)"</span><span class="sxs-lookup"><span data-stu-id="d3830-146">DASH: **Path** + manifest file name + "/manifest(format=mpd-time-csf)"</span></span>

<span data-ttu-id="d3830-147">Örnek:</span><span class="sxs-lookup"><span data-stu-id="d3830-147">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


### <a name="build-progressive-download-urls"></a><span data-ttu-id="d3830-148">Aşamalı indirme URL'leri derleme</span><span class="sxs-lookup"><span data-stu-id="d3830-148">Build progressive download URLs</span></span>
<span data-ttu-id="d3830-149">Kullanım hello **yolu** hello Bulucu toobuild hello aşamalı indirme URL'si hello oluşturulduktan sonra döndürülen değer.</span><span class="sxs-lookup"><span data-stu-id="d3830-149">Use hello **Path** value returned after hello creation of hello locator toobuild hello progressive download URL.</span></span>   

<span data-ttu-id="d3830-150">URL: **yolu** + varlık dosyası mp4 adı</span><span class="sxs-lookup"><span data-stu-id="d3830-150">URL: **Path** + asset file mp4 name</span></span>

<span data-ttu-id="d3830-151">Örnek:</span><span class="sxs-lookup"><span data-stu-id="d3830-151">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

## <span data-ttu-id="d3830-152"><a id="types"></a>Numaralandırma türleri</span><span class="sxs-lookup"><span data-stu-id="d3830-152"><a id="types"></a>Enum types</span></span>
    [Flags]
    public enum AccessPermissions
    {
        None = 0,
        Read = 1,
        Write = 2,
        Delete = 4,
        List = 8,
    }

    public enum LocatorType
    {
        None = 0,
        Sas = 1,
        OnDemandOrigin = 2,
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="d3830-153">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="d3830-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d3830-154">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="d3830-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="d3830-155">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="d3830-155">See also</span></span>
[<span data-ttu-id="d3830-156">Media Services operations REST API genel bakış</span><span class="sxs-lookup"><span data-stu-id="d3830-156">Media Services operations REST API overview</span></span>](media-services-rest-how-to-use.md)

[<span data-ttu-id="d3830-157">Varlık teslim ilkesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d3830-157">Configure asset delivery policy</span></span>](media-services-rest-configure-asset-delivery-policy.md)

