---
title: "Media Services REST API kullanarak aaaConfiguring varlık teslim ilkeleri | Microsoft Docs"
description: "Bu konuda gösterilmektedir nasıl Media Services REST API kullanarak tooconfigure farklı varlık teslim ilkeleri."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5cb9d32a-e68b-4585-aa82-58dded0691d0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 8203230d570935e17382c598820dbfe42f83f8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-asset-delivery-policies"></a><span data-ttu-id="d0bcd-103">Varlık teslim ilkeleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d0bcd-103">Configuring asset delivery policies</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

<span data-ttu-id="d0bcd-104">Dinamik olarak şifrelenmiş toodeliver varlıklar planlıyorsanız, hello birini hello medya Hizmetleri içerik teslim iş akışı varlıklar için teslim ilkelerini yapılandırma adımları.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-104">If you plan toodeliver dynamically encrypted assets, one of hello steps in hello Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="d0bcd-105">Merhaba varlık teslim ilkesini Media Services nasıl teslim, varlık toobe için istediğinizi söyler: toodynamically istediğiniz olup olmadığına bakılmaksızın hangi akış protokolüne Varlığınızı dinamik olarak (örneğin, MPEG DASH, HLS, kesintisiz akış veya tümü için), paketlenmiş Varlığınızı şifrelemek ve nasıl (Zarf veya ortak şifreleme).</span><span class="sxs-lookup"><span data-stu-id="d0bcd-105">hello asset delivery policy tells Media Services how you want for your asset toobe delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want toodynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="d0bcd-106">Bu konuda neden ve nasıl anlatılmaktadır toocreate ve varlık teslim ilkeleri yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-106">This topic discusses why and how toocreate and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="d0bcd-107">AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-107">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="d0bcd-108">İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-108">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
>
><span data-ttu-id="d0bcd-109">Ayrıca, toobe mümkün toouse dinamik paketleme ve dinamik şifreleme Varlığınızı içermelidir Uyarlamalı bit hızlı MP4s veya uyarlamalı bit hızlı kesintisiz akış dosyaları kümesidir.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-109">Also, toobe able toouse dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="d0bcd-110">Farklı ilkeleri toohello uygulayabilir aynı varlık.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-110">You could apply different policies toohello same asset.</span></span> <span data-ttu-id="d0bcd-111">Örneğin, PlayReady şifreleme tooSmooth akış ve AES zarfı şifreleme tooMPEG uygulayabilir DASH ve HLS.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-111">For example, you could apply PlayReady encryption tooSmooth Streaming and AES Envelope encryption tooMPEG DASH and HLS.</span></span> <span data-ttu-id="d0bcd-112">Bir teslim ilkesinde tanımlanmayan tüm protokollerin (örneğin, yalnızca hello protokol olarak HLS belirten tek bir ilke ekliyorsunuz) akışla aktarılması engellenir.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-112">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="d0bcd-113">Merhaba özel durum toothis hiç tanımlanmış hiçbir varlık teslim ilkesini varsa ' dir.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-113">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="d0bcd-114">Ardından, tüm protokoller hello Temizle izin verilir.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-114">Then, all protocols will be allowed in hello clear.</span></span>

<span data-ttu-id="d0bcd-115">Toodeliver depolama şifrelenmiş varlık isterseniz hello varlığın teslim ilkesini yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-115">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="d0bcd-116">Varlığınızı akışı önce sunucu kaldırır hello depolama şifrelemesi ve akışlar hello kullanarak içeriğinizi akış hello teslim ilkesini belirtilen.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-116">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="d0bcd-117">Örneğin, toodeliver Varlığınızı Gelişmiş Şifreleme Standardı (AES) Zarf şifreleme anahtarıyla şifrelenir, çok hello ilke türünü ayarlayın**DynamicEnvelopeEncryption**.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-117">For example, toodeliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set hello policy type too**DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="d0bcd-118">tooremove depolama şifreleme ve hello Temizle, akış hello varlığı ayarlamak hello ilke türü çok**NoDynamicEncryption**.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-118">tooremove storage encryption and stream hello asset in hello clear, set hello policy type too**NoDynamicEncryption**.</span></span> <span data-ttu-id="d0bcd-119">Bu ilke türleri tooconfigure nasıl izleyin Göster örnekleri.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-119">Examples that show how tooconfigure these policy types follow.</span></span>

<span data-ttu-id="d0bcd-120">Hello varlık teslim ilkesini nasıl yapılandırdığınıza bağlı mümkün toodynamically paketi, dinamik olarak şifrelemek ve akış akış protokolleri aşağıdaki hello: kesintisiz akış, HLS, MPEG DASH akışları.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-120">Depending on how you configure hello asset delivery policy you would be able toodynamically package, dynamically encrypt, and stream hello following streaming protocols: Smooth Streaming, HLS, MPEG DASH streams.</span></span>

<span data-ttu-id="d0bcd-121">Liste gösterir hello aşağıdaki hello toostream kesintisiz, HLS, DASH kullandığınız biçimlendirir.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-121">hello following list shows hello formats that you use toostream Smooth, HLS, DASH.</span></span>

<span data-ttu-id="d0bcd-122">Kesintisiz akış:</span><span class="sxs-lookup"><span data-stu-id="d0bcd-122">Smooth Streaming:</span></span>

<span data-ttu-id="d0bcd-123">{akış uç noktası adı-media services hesabı adı}.streaming.mediaservices.windows.net/{konum kimliği}/{dosya adı}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="d0bcd-123">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="d0bcd-124">HLS:</span><span class="sxs-lookup"><span data-stu-id="d0bcd-124">HLS:</span></span>

<span data-ttu-id="d0bcd-125">{uç nokta adı media services hesabı name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl) akış</span><span class="sxs-lookup"><span data-stu-id="d0bcd-125">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="d0bcd-126">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="d0bcd-126">MPEG DASH</span></span>

<span data-ttu-id="d0bcd-127">{uç nokta adı media services hesabı name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf) akış</span><span class="sxs-lookup"><span data-stu-id="d0bcd-127">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


<span data-ttu-id="d0bcd-128">Yönergeler için nasıl toopublish bir varlık ve yapı bir akış URL'si bkz [akış URL'si oluşturma](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="d0bcd-128">For instructions on how toopublish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="d0bcd-129">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="d0bcd-129">Considerations</span></span>
* <span data-ttu-id="d0bcd-130">Bu varlık için bir (akış) OnDemand Bulucu bulunmakla birlikte bir varlıkla ilişkilendirilen AssetDeliveryPolicy silemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="d0bcd-131">Merhaba tooremove hello hello varlık ilkesinden hello İlkesi silmeden önce önerilir.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-131">hello recommendation is tooremove hello policy from hello asset before deleting hello policy.</span></span>
* <span data-ttu-id="d0bcd-132">Hiçbir varlık teslim ilkesini ayarlandığında akış Bulucusu bir depolama şifrelenmiş varlık oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="d0bcd-133">Merhaba varlık şifrelenmiş depolama değilse, hello sistem, bir varlık teslim ilkesini olmadan temizleyin hello Bulucu ve akış hello varlık oluşturmak olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-133">If hello Asset isn’t storage encrypted, hello system will let you create a locator and stream hello asset in hello clear without an asset delivery policy.</span></span>
* <span data-ttu-id="d0bcd-134">Tek bir varlık ile ilişkili birden çok varlık teslim ilkeleri olabilir ancak yalnızca tek yönlü toohandle verilen AssetDeliveryProtocol belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way toohandle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="d0bcd-135">Bir istemci bir kesintisiz akış bir istekte bulunduğunda hello sistem hangisinin bilmediğinden, bir hatayla sonuçlanır hello AssetDeliveryProtocol.SmoothStreaming protokolü belirtmek toolink iki teslim İlkesi çalışırsanız anlamına tooapply istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-135">Meaning if you try toolink two delivery policies that specify hello AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because hello system does not know which one you want it tooapply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="d0bcd-136">Bir varlığı ile var olan bir akış Bulucu varsa, yeni bir ilke toohello varlık bağlantı olamaz, mevcut bir hello varlık ilkesinden bağlantısını veya hello varlık ile ilişkili bir teslim ilkesini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-136">If you have an asset with an existing streaming locator, you cannot link a new policy toohello asset, unlink an existing policy from hello asset, or update a delivery policy associated with hello asset.</span></span>  <span data-ttu-id="d0bcd-137">İlk tooremove hello akış Bulucusu sahip hello ilkeleri ayarlamak ve akış Bulucu hello yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-137">You first have tooremove hello streaming locator, adjust hello policies, and then re-create hello streaming locator.</span></span>  <span data-ttu-id="d0bcd-138">İçerik hello Menşe veya bir aşağı akış CDN tarafından önbelleğe bu yana, istemciler için sorunlara neden olmaz Bulucu ancak Akış hello yeniden oluşturduğunuzda aynı locatorId emin olmalısınız hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-138">You can use hello same locatorId when you recreate hello streaming locator but you should ensure that won’t cause issues for clients since content can be cached by hello origin or a downstream CDN.</span></span>

>[!NOTE]

><span data-ttu-id="d0bcd-139">Varlıklar Media Services erişirken, HTTP istekleri özel üstbilgi alanlarını ve değerlerini ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-139">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="d0bcd-140">Daha fazla bilgi için bkz: [Media Services REST API geliştirme için Kurulum](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="d0bcd-140">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="d0bcd-141">TooMedia Hizmetleri'ne Bağlama</span><span class="sxs-lookup"><span data-stu-id="d0bcd-141">Connect tooMedia Services</span></span>

<span data-ttu-id="d0bcd-142">Nasıl tooconnect toohello AMS API, bkz. bilgi [Azure AD kimlik doğrulaması ile erişim hello Azure Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="d0bcd-142">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="d0bcd-143">Başarıyla toohttps://media.windows.net bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-143">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="d0bcd-144">Sonraki çağrılar toohello yapmanız gereken yeni bir URI.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-144">You must make subsequent calls toohello new URI.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="d0bcd-145">Clear varlık teslim ilkesini</span><span class="sxs-lookup"><span data-stu-id="d0bcd-145">Clear asset delivery policy</span></span>
### <span data-ttu-id="d0bcd-146"><a id="create_asset_delivery_policy"></a>Varlık teslim ilkesini oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0bcd-146"><a id="create_asset_delivery_policy"></a>Create asset delivery policy</span></span>
<span data-ttu-id="d0bcd-147">Hello aşağıdaki HTTP isteği toonot dinamik şifreleme uygulanır ve aşağıdaki hello hiçbirinde toodeliver hello akış protokolleri belirten bir varlık teslim ilkesi oluşturur: MPEG DASH, HLS ve kesintisiz akış protokollerini.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-147">hello following HTTP request creates an asset delivery policy that specifies toonot apply dynamic encryption and toodeliver hello stream in any of hello following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> 

<span data-ttu-id="d0bcd-148">Merhaba, değerleri bilgi bir AssetDeliveryPolicy oluştururken belirtebilirsiniz için bkz: [AssetDeliveryPolicy tanımlarken kullanılan türleri](#types) bölümü.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-148">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="d0bcd-149">İsteği:</span><span class="sxs-lookup"><span data-stu-id="d0bcd-149">Request:</span></span>

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    Host: media.windows.net

    {"Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null}

<span data-ttu-id="d0bcd-150">Yanıtı:</span><span class="sxs-lookup"><span data-stu-id="d0bcd-150">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 363
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    x-ms-request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 06:21:27 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element",
    "Id":"nb:adpid:UUID:92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd",
    "Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null,
    "Created":"2015-02-08T06:21:27.6908329Z",
    "LastModified":"2015-02-08T06:21:27.6908329Z"}

### <span data-ttu-id="d0bcd-151"><a id="link_asset_with_asset_delivery_policy"></a>Varlık teslim ilkesini bağlantı varlığı</span><span class="sxs-lookup"><span data-stu-id="d0bcd-151"><a id="link_asset_with_asset_delivery_policy"></a>Link asset with asset delivery policy</span></span>
<span data-ttu-id="d0bcd-152">HTTP isteği bağlantılar hello aşağıdaki hello varlık toohello varlık teslim ilkesini için belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-152">hello following HTTP request links hello specified asset toohello asset delivery policy to.</span></span>

<span data-ttu-id="d0bcd-153">İsteği:</span><span class="sxs-lookup"><span data-stu-id="d0bcd-153">Request:</span></span>

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A86933344-9539-4d0c-be7d-f842458693e0')/$links/DeliveryPolicies HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-3344-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 56d2763f-6e72-419d-ba3c-685f6db97e81
    Host: media.windows.net

    {"uri":"https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')"}

<span data-ttu-id="d0bcd-154">Yanıtı:</span><span class="sxs-lookup"><span data-stu-id="d0bcd-154">Response:</span></span>

    HTTP/1.1 204 No Content


## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="d0bcd-155">DynamicEnvelopeEncryption varlık teslim ilkesini</span><span class="sxs-lookup"><span data-stu-id="d0bcd-155">DynamicEnvelopeEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-hello-envelopeencryption-type-and-link-it-toohello-asset"></a><span data-ttu-id="d0bcd-156">Merhaba EnvelopeEncryption tür içerik anahtarı oluşturun ve toohello varlık Bağla</span><span class="sxs-lookup"><span data-stu-id="d0bcd-156">Create content key of hello EnvelopeEncryption type and link it toohello asset</span></span>
<span data-ttu-id="d0bcd-157">DynamicEnvelopeEncryption teslim İlkesi belirtirken, varlık tooa içerik anahtarı hello EnvelopeEncryption türü toomake emin toolink gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-157">When specifying DynamicEnvelopeEncryption delivery policy, you need toomake sure toolink your asset tooa content key of hello EnvelopeEncryption type.</span></span> <span data-ttu-id="d0bcd-158">Daha fazla bilgi için bkz: [bir içerik anahtarı oluşturma](media-services-rest-create-contentkey.md)).</span><span class="sxs-lookup"><span data-stu-id="d0bcd-158">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <span data-ttu-id="d0bcd-159"><a id="get_delivery_url"></a>Teslim URL'sini alma</span><span class="sxs-lookup"><span data-stu-id="d0bcd-159"><a id="get_delivery_url"></a>Get delivery URL</span></span>
<span data-ttu-id="d0bcd-160">Get hello teslim hello URL'sini hello içerik anahtarı hello önceki adımda oluşturduğunuz teslim yöntemi belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-160">Get hello delivery URL for hello specified delivery method of hello content key created in hello previous step.</span></span> <span data-ttu-id="d0bcd-161">URL toorequest döndürülen hello bir istemcinin kullandığı bir AES anahtarı ya da bir sipariş tooplayback hello PlayReady lisans korumalı içeriği.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-161">A client uses hello returned URL toorequest an AES key or a PlayReady license in order tooplayback hello protected content.</span></span>

<span data-ttu-id="d0bcd-162">Merhaba URL tooget Hello türü hello hello HTTP isteğinin gövdesinde belirtin.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-162">Specify hello type of hello URL tooget in hello body of hello HTTP request.</span></span> <span data-ttu-id="d0bcd-163">Bir Media Services PlayReady lisans edinme URL'si isteği içeriğinizi PlayReady ile koruyorsanız 1 hello keyDeliveryType kullanılarak: {"keyDeliveryType": 1}.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-163">If you are protecting your content with PlayReady, request a Media Services PlayReady license acquisition URL, using 1 for hello keyDeliveryType: {"keyDeliveryType":1}.</span></span> <span data-ttu-id="d0bcd-164">İçeriğinizi hello Zarf şifrelemeli koruyorsanız, bir anahtar alım keyDeliveryType için 2 belirterek istek URL'si: {"keyDeliveryType": 2}.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-164">If you are protecting your content with hello envelope encryption, request a key acquisition URL by specifying 2 for keyDeliveryType: {"keyDeliveryType":2}.</span></span>

<span data-ttu-id="d0bcd-165">İsteği:</span><span class="sxs-lookup"><span data-stu-id="d0bcd-165">Request:</span></span>

    POST https://media.windows.net/api/ContentKeys('nb:kid:UUID:dc88f996-2859-4cf7-a279-c52a9d6b2f04')/GetKeyDeliveryUrl HTTP/1.1
    Content-Type: application/json
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423452029&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=IEXV06e3drSIN5naFRBdhJZCbfEqQbFZsGSIGmawhEo%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    Host: media.windows.net
    Content-Length: 21

    {"keyDeliveryType":2}

<span data-ttu-id="d0bcd-166">Yanıtı:</span><span class="sxs-lookup"><span data-stu-id="d0bcd-166">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 198
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    x-ms-request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 21:42:30 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#Edm.String","value":"https://amsaccount1.keydelivery.mediaservices.windows.net/?KID=dc88f996-2859-4cf7-a279-c52a9d6b2f04"}


### <a name="create-asset-delivery-policy"></a><span data-ttu-id="d0bcd-167">Varlık teslim ilkesini oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0bcd-167">Create asset delivery policy</span></span>
<span data-ttu-id="d0bcd-168">Merhaba aşağıdaki HTTP isteği oluşturur hello **AssetDeliveryPolicy** diğer bir deyişle yapılandırılmış tooapply dinamik Zarf şifreleme (**DynamicEnvelopeEncryption**) toohello **HLS**Protokolü (Bu örnekte, diğer protokolleri akışla aktarılması engellenir).</span><span class="sxs-lookup"><span data-stu-id="d0bcd-168">hello following HTTP request creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic envelope encryption (**DynamicEnvelopeEncryption**) toohello **HLS** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="d0bcd-169">Merhaba, değerleri bilgi bir AssetDeliveryPolicy oluştururken belirtebilirsiniz için bkz: [AssetDeliveryPolicy tanımlarken kullanılan türleri](#types) bölümü.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-169">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="d0bcd-170">İsteği:</span><span class="sxs-lookup"><span data-stu-id="d0bcd-170">Request:</span></span>

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]"}


<span data-ttu-id="d0bcd-171">Yanıtı:</span><span class="sxs-lookup"><span data-stu-id="d0bcd-171">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 460
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3Aec9b994e-672c-4a5b-8490-a464eeb7964b')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    x-ms-request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 09 Feb 2015 05:24:38 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element","Id":"nb:adpid:UUID:ec9b994e-672c-4a5b-8490-a464eeb7964b","Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]","Created":"2015-02-09T05:24:38.9167436Z","LastModified":"2015-02-09T05:24:38.9167436Z"}


### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="d0bcd-172">Varlık teslim ilkesini bağlantı varlığı</span><span class="sxs-lookup"><span data-stu-id="d0bcd-172">Link asset with asset delivery policy</span></span>
<span data-ttu-id="d0bcd-173">Bkz: [varlık teslim ilkesini bağlantı varlığı](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="d0bcd-173">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="d0bcd-174">DynamicCommonEncryption varlık teslim ilkesini</span><span class="sxs-lookup"><span data-stu-id="d0bcd-174">DynamicCommonEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-hello-commonencryption-type-and-link-it-toohello-asset"></a><span data-ttu-id="d0bcd-175">Merhaba CommonEncryption tür içerik anahtarı oluşturun ve toohello varlık Bağla</span><span class="sxs-lookup"><span data-stu-id="d0bcd-175">Create content key of hello CommonEncryption type and link it toohello asset</span></span>
<span data-ttu-id="d0bcd-176">DynamicCommonEncryption teslim İlkesi belirtirken, varlık tooa içerik anahtarı hello CommonEncryption türü toomake emin toolink gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-176">When specifying DynamicCommonEncryption delivery policy, you need toomake sure toolink your asset tooa content key of hello CommonEncryption type.</span></span> <span data-ttu-id="d0bcd-177">Daha fazla bilgi için bkz: [bir içerik anahtarı oluşturma](media-services-rest-create-contentkey.md)).</span><span class="sxs-lookup"><span data-stu-id="d0bcd-177">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <a name="get-delivery-url"></a><span data-ttu-id="d0bcd-178">Teslim URL'sini alma</span><span class="sxs-lookup"><span data-stu-id="d0bcd-178">Get Delivery URL</span></span>
<span data-ttu-id="d0bcd-179">Merhaba PlayReady teslim yöntemini hello içerik anahtarının hello önceki adımda oluşturduğunuz Hello teslim URL'sini alma.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-179">Get hello delivery URL for hello PlayReady delivery method of hello content key created in hello previous step.</span></span> <span data-ttu-id="d0bcd-180">Bir istemci bir sipariş tooplayback hello PlayReady lisans korumalı URL toorequest içerik döndürülen hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-180">A client uses hello returned URL toorequest a PlayReady license in order tooplayback hello protected content.</span></span> <span data-ttu-id="d0bcd-181">Daha fazla bilgi için bkz: [alma teslim URL](#get_delivery_url).</span><span class="sxs-lookup"><span data-stu-id="d0bcd-181">For more information, see [Get Delivery URL](#get_delivery_url).</span></span>

### <a name="create-asset-delivery-policy"></a><span data-ttu-id="d0bcd-182">Varlık teslim ilkesini oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0bcd-182">Create asset delivery policy</span></span>
<span data-ttu-id="d0bcd-183">Merhaba aşağıdaki HTTP isteği oluşturur hello **AssetDeliveryPolicy** diğer bir deyişle yapılandırılmış tooapply dinamik ortak şifreleme (**DynamicCommonEncryption**) toohello **kesintisiz akış**  Protokolü (Bu örnekte, diğer protokolleri akışla aktarılması engellenir).</span><span class="sxs-lookup"><span data-stu-id="d0bcd-183">hello following HTTP request creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic common encryption (**DynamicCommonEncryption**) toohello **Smooth Streaming** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="d0bcd-184">Merhaba, değerleri bilgi bir AssetDeliveryPolicy oluştururken belirtebilirsiniz için bkz: [AssetDeliveryPolicy tanımlarken kullanılan türleri](#types) bölümü.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-184">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="d0bcd-185">İsteği:</span><span class="sxs-lookup"><span data-stu-id="d0bcd-185">Request:</span></span>

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":1,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\/PlayReady\/"}]"}


<span data-ttu-id="d0bcd-186">Widevine DRM kullanarak içeriğinizi tooprotect istiyorsanız hello AssetDeliveryConfiguration değerleri toouse (7 hello değeri olan) WidevineLicenseAcquisitionUrl güncelleştirin ve bir lisans teslimat hizmetinin hello URL'sini belirtin.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-186">If you want tooprotect your content using Widevine DRM, update hello AssetDeliveryConfiguration values toouse WidevineLicenseAcquisitionUrl (which has hello value of 7) and specify hello URL of a license delivery service.</span></span> <span data-ttu-id="d0bcd-187">Widevine lisansları teslim AMS ortaklarını toohelp aşağıdaki hello kullanabilirsiniz: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="d0bcd-187">You can use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="d0bcd-188">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="d0bcd-188">For example:</span></span> 

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":2,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":7,\"Value\":\"https:\\/\\/example.net\/WidevineLicenseAcquisition\/"}]"}

> [!NOTE]
> <span data-ttu-id="d0bcd-189">Widevine ile şifrelerken tire kullanarak mümkün toodeliver yalnızca olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-189">When encrypting with Widevine, you would only be able toodeliver using DASH.</span></span> <span data-ttu-id="d0bcd-190">Emin toospecify tire (2) içinde hello varlık teslim Protokolü olun.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-190">Make sure toospecify DASH (2) in hello asset delivery protocol.</span></span>
> 
> 

### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="d0bcd-191">Varlık teslim ilkesini bağlantı varlığı</span><span class="sxs-lookup"><span data-stu-id="d0bcd-191">Link asset with asset delivery policy</span></span>
<span data-ttu-id="d0bcd-192">Bkz: [varlık teslim ilkesini bağlantı varlığı](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="d0bcd-192">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <span data-ttu-id="d0bcd-193"><a id="types"></a>AssetDeliveryPolicy tanımlarken kullanılan türleri</span><span class="sxs-lookup"><span data-stu-id="d0bcd-193"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <a name="assetdeliveryprotocol"></a><span data-ttu-id="d0bcd-194">AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="d0bcd-194">AssetDeliveryProtocol</span></span>

<span data-ttu-id="d0bcd-195">Merhaba aşağıdaki enum hello varlık teslim protokolü için ayarlayabileceğiniz değerler açıklar.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-195">hello following enum describes values you can set for hello asset delivery protocol.</span></span>

    [Flags]
    public enum AssetDeliveryProtocol
    {
        /// <summary>
        /// No protocols.
        /// </summary>
        None = 0x0,

        /// <summary>
        /// Smooth streaming protocol.
        /// </summary>
        SmoothStreaming = 0x1,

        /// <summary>
        /// MPEG Dynamic Adaptive Streaming over HTTP (DASH)
        /// </summary>
        Dash = 0x2,

        /// <summary>
        /// Apple HTTP Live Streaming protocol.
        /// </summary>
        HLS = 0x4,

        ProgressiveDownload = 0x10, 
 
        /// <summary>
        /// Include all protocols.
        /// </summary>
        All = 0xFFFF
    }

### <a name="assetdeliverypolicytype"></a><span data-ttu-id="d0bcd-196">AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="d0bcd-196">AssetDeliveryPolicyType</span></span>

<span data-ttu-id="d0bcd-197">Merhaba aşağıdaki enum hello varlık teslim İlkesi türü için ayarlayabileceğiniz değerler açıklar.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-197">hello following enum describes values you can set for hello asset delivery policy type.</span></span>  

    public enum AssetDeliveryPolicyType
    {
        /// <summary>
        /// Delivery Policy Type not set.  An invalid value.
        /// </summary>
        None,

        /// <summary>
        /// hello Asset should not be delivered via this AssetDeliveryProtocol. 
        /// </summary>
        Blocked, 

        /// <summary>
        /// Do not apply dynamic encryption toohello asset.
        /// </summary>
        /// 
        NoDynamicEncryption,  

        /// <summary>
        /// Apply Dynamic Envelope encryption.
        /// </summary>
        DynamicEnvelopeEncryption,

        /// <summary>
        /// Apply Dynamic Common encryption.
        /// </summary>
        DynamicCommonEncryption
        }

### <a name="contentkeydeliverytype"></a><span data-ttu-id="d0bcd-198">ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="d0bcd-198">ContentKeyDeliveryType</span></span>

<span data-ttu-id="d0bcd-199">Merhaba aşağıdaki enum değerleri hello içerik anahtar toohello istemci tooconfigure hello teslim yöntemini kullanabilirsiniz açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-199">hello following enum describes values you can use tooconfigure hello delivery method of hello content key toohello client.</span></span>
    
    public enum ContentKeyDeliveryType
    {
        /// <summary>
        /// None.
        ///
        </summary>
        None = 0,

        /// <summary>
        /// Use PlayReady License acquistion protocol
        ///
        </summary>
        PlayReadyLicense = 1,

        /// <summary>
        /// Use MPEG Baseline HTTP key protocol.
        ///
        </summary>
        BaselineHttp = 2,

        /// <summary>
        /// Use Widevine License acquistion protocol
        ///
        </summary>
        Widevine = 3

    }


### <a name="assetdeliverypolicyconfigurationkey"></a><span data-ttu-id="d0bcd-200">AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="d0bcd-200">AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="d0bcd-201">Enum aşağıdaki hello tooconfigure kullanılan anahtarları tooget belirli yapılandırma için bir varlık teslim ilkesini ayarlayabilirsiniz değerleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d0bcd-201">hello following enum describes values you can set tooconfigure keys used tooget specific configuration for an asset delivery policy.</span></span>

    public enum AssetDeliveryPolicyConfigurationKey
    {
        /// <summary>
        /// No policies.
        /// </summary>
        None,

        /// <summary>
        /// Exact Envelope key URL.
        /// </summary>
        EnvelopeKeyAcquisitionUrl,

        /// <summary>
        /// Base key url that will have KID=<Guid> appended for Envelope.
        /// </summary>
        EnvelopeBaseKeyAcquisitionUrl,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption in Base64 format.
        /// </summary>
        EnvelopeEncryptionIVAsBase64,

        /// <summary>
        /// hello PlayReady License Acquisition Url toouse for common encryption.
        /// </summary>
        PlayReadyLicenseAcquisitionUrl,

        /// <summary>
        /// hello PlayReady Custom Attributes tooadd toohello PlayReady Content Header
        /// </summary>
        PlayReadyCustomAttributes,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption.
        /// </summary>
        EnvelopeEncryptionIV,

        /// <summary>
        /// Widevine DRM acquisition url
        /// </summary>
        WidevineLicenseAcquisitionUrl
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="d0bcd-202">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="d0bcd-202">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d0bcd-203">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="d0bcd-203">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

