---
title: "Media Services REST API kullanarak varlık teslim ilkeleri yapılandırma | Microsoft Docs"
description: "Bu konu, Media Services REST API kullanarak farklı varlık teslim ilkelerinin nasıl yapılandırılacağını gösterir."
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
ms.openlocfilehash: 7ffbde11b943961dd3a3b5edebd0cfd52429e845
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-asset-delivery-policies"></a><span data-ttu-id="23029-103">Varlık teslim ilkeleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="23029-103">Configuring asset delivery policies</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

<span data-ttu-id="23029-104">Dinamik olarak şifrelenmiş varlıklar iletmeyi planlıyorsanız, Media Services içerik teslim iş akışı'ndaki adımları birini varlıklar için teslim ilkeleri yapılandırıyor.</span><span class="sxs-lookup"><span data-stu-id="23029-104">If you plan to deliver dynamically encrypted assets, one of the steps in the Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="23029-105">Media Services, varlık teslim edilmesini istediğiniz varlık teslim ilkesini bildirir: hangi Akış Protokolü varlığınız dinamik olarak paketlenir (örneğin, MPEG DASH, HLS, kesintisiz akış veya tümü için), dinamik olarak Varlığınızı şifrelemek isteyip istemediğinizi ve nasıl içine (Zarf veya ortak şifreleme).</span><span class="sxs-lookup"><span data-stu-id="23029-105">The asset delivery policy tells Media Services how you want for your asset to be delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want to dynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="23029-106">Bu konuda ele alınmıştır neden ve nasıl oluşturulacağı ve varlık teslim ilkeleri yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="23029-106">This topic discusses why and how to create and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="23029-107">AMS hesabınız oluşturulduğunda hesabınıza **Durdurulmuş** durumda bir **varsayılan** akış uç noktası eklenir.</span><span class="sxs-lookup"><span data-stu-id="23029-107">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="23029-108">İçerik akışını başlatmak ve dinamik paketleme ile dinamik şifrelemeden yararlanmak için içerik akışı yapmak istediğiniz akış uç noktasının **Çalışıyor** durumda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="23029-108">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 
>
><span data-ttu-id="23029-109">Ayrıca, dinamik paketleme ve dinamik şifreleme kullanabilmek için varlığınız Uyarlamalı bit hızlı MP4s ya da Uyarlamalı bit hızlı kesintisiz akış dosyaları içermelidir.</span><span class="sxs-lookup"><span data-stu-id="23029-109">Also, to be able to use dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="23029-110">Aynı varlık için farklı ilkeler uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23029-110">You could apply different policies to the same asset.</span></span> <span data-ttu-id="23029-111">Örneğin, MPEG DASH ve HLS için AES zarfı kesintisiz akış ve şifreleme için PlayReady şifreleme uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23029-111">For example, you could apply PlayReady encryption to Smooth Streaming and AES Envelope encryption to MPEG DASH and HLS.</span></span> <span data-ttu-id="23029-112">Herhangi bir teslim ilkesinde tanımlanmayan tüm protokollerin (örneğin, protokol olarak yalnızca HLS‘yi belirten tek bir ilke ekliyorsunuz) akışla aktarılması engellenir.</span><span class="sxs-lookup"><span data-stu-id="23029-112">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as the protocol) will be blocked from streaming.</span></span> <span data-ttu-id="23029-113">Bunun tek istisnası, hiçbir varlık teslim ilkesinin tanımlanmadığı durumdur.</span><span class="sxs-lookup"><span data-stu-id="23029-113">The exception to this is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="23029-114">Bu halde tüm protokollere açık bir şekilde izin verilir.</span><span class="sxs-lookup"><span data-stu-id="23029-114">Then, all protocols will be allowed in the clear.</span></span>

<span data-ttu-id="23029-115">Bir depolama şifrelenmiş varlık teslim etmek istiyorsanız, varlığın teslim ilkesini yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="23029-115">If you want to deliver a storage encrypted asset, you must configure the asset’s delivery policy.</span></span> <span data-ttu-id="23029-116">Varlığınızı akışı önce akış sunucusu depolama şifreleme kaldırır ve belirtilen teslim ilkesini kullanarak içeriğinizi akışlarını.</span><span class="sxs-lookup"><span data-stu-id="23029-116">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy.</span></span> <span data-ttu-id="23029-117">Örneğin, Gelişmiş Şifreleme Standardı (AES) Zarf şifreleme anahtarıyla şifrelenir, varlık teslim etmek için ilke türünü ayarlamak **DynamicEnvelopeEncryption**.</span><span class="sxs-lookup"><span data-stu-id="23029-117">For example, to deliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set the policy type to **DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="23029-118">Depolama şifrelemesi kaldırmak ve varlık temiz akışını ilke türünü ayarlayın **NoDynamicEncryption**.</span><span class="sxs-lookup"><span data-stu-id="23029-118">To remove storage encryption and stream the asset in the clear, set the policy type to **NoDynamicEncryption**.</span></span> <span data-ttu-id="23029-119">Bu ilke türünü yapılandırmanız nasıl gösteren örnekler izleyin.</span><span class="sxs-lookup"><span data-stu-id="23029-119">Examples that show how to configure these policy types follow.</span></span>

<span data-ttu-id="23029-120">Varlık teslim ilkesini nasıl yapılandırdığınıza bağlı olarak, dinamik olarak paketini, dinamik olarak şifrelemek ve aşağıdaki akış protokolleri akışını gerçekleştirebilir: kesintisiz akış, HLS, MPEG DASH akışları.</span><span class="sxs-lookup"><span data-stu-id="23029-120">Depending on how you configure the asset delivery policy you would be able to dynamically package, dynamically encrypt, and stream the following streaming protocols: Smooth Streaming, HLS, MPEG DASH streams.</span></span>

<span data-ttu-id="23029-121">Aşağıdaki liste, akışa kesintisiz, HLS, DASH kullandığınız biçimleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="23029-121">The following list shows the formats that you use to stream Smooth, HLS, DASH.</span></span>

<span data-ttu-id="23029-122">Kesintisiz akış:</span><span class="sxs-lookup"><span data-stu-id="23029-122">Smooth Streaming:</span></span>

<span data-ttu-id="23029-123">{akış uç noktası adı-media services hesabı adı}.streaming.mediaservices.windows.net/{konum kimliği}/{dosya adı}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="23029-123">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="23029-124">HLS:</span><span class="sxs-lookup"><span data-stu-id="23029-124">HLS:</span></span>

<span data-ttu-id="23029-125">{uç nokta adı media services hesabı name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl) akış</span><span class="sxs-lookup"><span data-stu-id="23029-125">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="23029-126">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="23029-126">MPEG DASH</span></span>

<span data-ttu-id="23029-127">{uç nokta adı media services hesabı name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf) akış</span><span class="sxs-lookup"><span data-stu-id="23029-127">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


<span data-ttu-id="23029-128">Varlık yayımlama ve akış URL'si oluşturma yönergeleri için bkz. [Akış URL'si oluşturma](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="23029-128">For instructions on how to publish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="23029-129">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="23029-129">Considerations</span></span>
* <span data-ttu-id="23029-130">Bu varlık için bir (akış) OnDemand Bulucu bulunmakla birlikte bir varlıkla ilişkilendirilen AssetDeliveryPolicy silemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="23029-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="23029-131">İlke silmeden önce varlığından ilkesini kaldırmak için önerilir.</span><span class="sxs-lookup"><span data-stu-id="23029-131">The recommendation is to remove the policy from the asset before deleting the policy.</span></span>
* <span data-ttu-id="23029-132">Hiçbir varlık teslim ilkesini ayarlandığında akış Bulucusu bir depolama şifrelenmiş varlık oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="23029-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="23029-133">Varlık şifrelenmiş depolama yoksa, sistem, bir Bulucu oluşturmanız ve varlık bir varlık teslim ilkesini olmadan temiz akışını olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="23029-133">If the Asset isn’t storage encrypted, the system will let you create a locator and stream the asset in the clear without an asset delivery policy.</span></span>
* <span data-ttu-id="23029-134">Tek bir varlık ile ilişkili birden çok varlık teslim ilkeleri olabilir, ancak yalnızca belirli bir AssetDeliveryProtocol işlemek için bir yol belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23029-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way to handle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="23029-135">Sistem hangisinin, bir istemci bir kesintisiz akış bir istekte bulunduğunda uygulanacak bilmediğinden, bir hatayla sonuçlanır AssetDeliveryProtocol.SmoothStreaming protokolü belirtmek iki teslim ilkeleri bağlamaya çalışır anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="23029-135">Meaning if you try to link two delivery policies that specify the AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because the system does not know which one you want it to apply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="23029-136">Bir varlığı ile var olan bir akış Bulucu varsa, yeni bir ilke varlık için bağlantı olamaz, mevcut bir varlık ilkesinden bağlantısını veya varlık ile ilişkili bir teslim ilkesini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="23029-136">If you have an asset with an existing streaming locator, you cannot link a new policy to the asset, unlink an existing policy from the asset, or update a delivery policy associated with the asset.</span></span>  <span data-ttu-id="23029-137">İlk bu akış Bulucusu kaldırmak, ilkeleri ayarlamak ve akış Bulucusu yeniden oluşturmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="23029-137">You first have to remove the streaming locator, adjust the policies, and then re-create the streaming locator.</span></span>  <span data-ttu-id="23029-138">Akış Bulucusu yeniden oluşturur ancak içerik kaynağı veya bir aşağı akış CDN tarafından önbelleğe beri sorunları istemciler için neden olmaz emin olmalısınız aynı locatorId kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23029-138">You can use the same locatorId when you recreate the streaming locator but you should ensure that won’t cause issues for clients since content can be cached by the origin or a downstream CDN.</span></span>

>[!NOTE]

><span data-ttu-id="23029-139">Varlıklar Media Services erişirken, HTTP istekleri özel üstbilgi alanlarını ve değerlerini ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="23029-139">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="23029-140">Daha fazla bilgi için bkz: [Media Services REST API geliştirme için Kurulum](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="23029-140">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="23029-141">Media Services’e bağlanmak</span><span class="sxs-lookup"><span data-stu-id="23029-141">Connect to Media Services</span></span>

<span data-ttu-id="23029-142">AMS API'sine bağlanma hakkında daha fazla bilgi için bkz: [Azure AD kimlik doğrulaması ile Azure Media Services API erişim](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="23029-142">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="23029-143">Başarıyla https://media.windows.net için bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız.</span><span class="sxs-lookup"><span data-stu-id="23029-143">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="23029-144">Yeni bir URI yapılan sonraki çağrılar yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="23029-144">You must make subsequent calls to the new URI.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="23029-145">Clear varlık teslim ilkesini</span><span class="sxs-lookup"><span data-stu-id="23029-145">Clear asset delivery policy</span></span>
### <span data-ttu-id="23029-146"><a id="create_asset_delivery_policy"></a>Varlık teslim ilkesini oluşturma</span><span class="sxs-lookup"><span data-stu-id="23029-146"><a id="create_asset_delivery_policy"></a>Create asset delivery policy</span></span>
<span data-ttu-id="23029-147">Aşağıdaki HTTP isteğini belirtir dinamik şifreleme uygulamamayı ve aşağıdaki protokollerden birini akışta teslim etmek için bir varlık teslim ilkesini oluşturur: MPEG DASH, HLS ve kesintisiz akış protokollerini.</span><span class="sxs-lookup"><span data-stu-id="23029-147">The following HTTP request creates an asset delivery policy that specifies to not apply dynamic encryption and to deliver the stream in any of the following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> 

<span data-ttu-id="23029-148">Bir AssetDeliveryPolicy oluştururken belirtebilirsiniz değerleri hakkında bilgi için bkz: [AssetDeliveryPolicy tanımlarken kullanılan türleri](#types) bölümü.</span><span class="sxs-lookup"><span data-stu-id="23029-148">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="23029-149">İsteği:</span><span class="sxs-lookup"><span data-stu-id="23029-149">Request:</span></span>

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

<span data-ttu-id="23029-150">Yanıtı:</span><span class="sxs-lookup"><span data-stu-id="23029-150">Response:</span></span>

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

### <span data-ttu-id="23029-151"><a id="link_asset_with_asset_delivery_policy"></a>Varlık teslim ilkesini bağlantı varlığı</span><span class="sxs-lookup"><span data-stu-id="23029-151"><a id="link_asset_with_asset_delivery_policy"></a>Link asset with asset delivery policy</span></span>
<span data-ttu-id="23029-152">Aşağıdaki HTTP isteği belirtilen varlık için varlık teslim ilkesini bağlar.</span><span class="sxs-lookup"><span data-stu-id="23029-152">The following HTTP request links the specified asset to the asset delivery policy to.</span></span>

<span data-ttu-id="23029-153">İsteği:</span><span class="sxs-lookup"><span data-stu-id="23029-153">Request:</span></span>

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

<span data-ttu-id="23029-154">Yanıtı:</span><span class="sxs-lookup"><span data-stu-id="23029-154">Response:</span></span>

    HTTP/1.1 204 No Content


## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="23029-155">DynamicEnvelopeEncryption varlık teslim ilkesini</span><span class="sxs-lookup"><span data-stu-id="23029-155">DynamicEnvelopeEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-the-envelopeencryption-type-and-link-it-to-the-asset"></a><span data-ttu-id="23029-156">EnvelopeEncryption tür içerik anahtarı oluşturup varlık için Bağla</span><span class="sxs-lookup"><span data-stu-id="23029-156">Create content key of the EnvelopeEncryption type and link it to the asset</span></span>
<span data-ttu-id="23029-157">DynamicEnvelopeEncryption teslim İlkesi belirtirken, varlık EnvelopeEncryption türü için bir içerik anahtarı bağlamak emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="23029-157">When specifying DynamicEnvelopeEncryption delivery policy, you need to make sure to link your asset to a content key of the EnvelopeEncryption type.</span></span> <span data-ttu-id="23029-158">Daha fazla bilgi için bkz: [bir içerik anahtarı oluşturma](media-services-rest-create-contentkey.md)).</span><span class="sxs-lookup"><span data-stu-id="23029-158">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <span data-ttu-id="23029-159"><a id="get_delivery_url"></a>Teslim URL'sini alma</span><span class="sxs-lookup"><span data-stu-id="23029-159"><a id="get_delivery_url"></a>Get delivery URL</span></span>
<span data-ttu-id="23029-160">Önceki adımda oluşturduğunuz içerik anahtarı belirtilen teslim yöntemini teslim URL'sini alma.</span><span class="sxs-lookup"><span data-stu-id="23029-160">Get the delivery URL for the specified delivery method of the content key created in the previous step.</span></span> <span data-ttu-id="23029-161">Bir PlayReady korumalı içeriği kayıttan yürütme sırada lisans ya da bir istemci bir AES anahtarı istemek için döndürülen URL kullanır.</span><span class="sxs-lookup"><span data-stu-id="23029-161">A client uses the returned URL to request an AES key or a PlayReady license in order to playback the protected content.</span></span>

<span data-ttu-id="23029-162">HTTP istek gövdesinde almak için URL'yi türünü belirtin.</span><span class="sxs-lookup"><span data-stu-id="23029-162">Specify the type of the URL to get in the body of the HTTP request.</span></span> <span data-ttu-id="23029-163">Bir Media Services PlayReady lisans edinme URL'si isteği içeriğinizi PlayReady ile koruyorsanız 1 için keyDeliveryType kullanılarak: {"keyDeliveryType": 1}.</span><span class="sxs-lookup"><span data-stu-id="23029-163">If you are protecting your content with PlayReady, request a Media Services PlayReady license acquisition URL, using 1 for the keyDeliveryType: {"keyDeliveryType":1}.</span></span> <span data-ttu-id="23029-164">İçeriğinizi Zarf şifrelemeli koruyorsanız, bir anahtar alım keyDeliveryType için 2 belirterek istek URL'si: {"keyDeliveryType": 2}.</span><span class="sxs-lookup"><span data-stu-id="23029-164">If you are protecting your content with the envelope encryption, request a key acquisition URL by specifying 2 for keyDeliveryType: {"keyDeliveryType":2}.</span></span>

<span data-ttu-id="23029-165">İsteği:</span><span class="sxs-lookup"><span data-stu-id="23029-165">Request:</span></span>

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

<span data-ttu-id="23029-166">Yanıtı:</span><span class="sxs-lookup"><span data-stu-id="23029-166">Response:</span></span>

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


### <a name="create-asset-delivery-policy"></a><span data-ttu-id="23029-167">Varlık teslim ilkesini oluşturma</span><span class="sxs-lookup"><span data-stu-id="23029-167">Create asset delivery policy</span></span>
<span data-ttu-id="23029-168">Aşağıdaki HTTP isteği oluşturur **AssetDeliveryPolicy** dinamik Zarf şifreleme uygulamak için yapılandırılmış (**DynamicEnvelopeEncryption**) için **HLS** Protokolü (Bu örnekte, diğer protokolleri akışla aktarılması engellenir).</span><span class="sxs-lookup"><span data-stu-id="23029-168">The following HTTP request creates the **AssetDeliveryPolicy** that is configured to apply dynamic envelope encryption (**DynamicEnvelopeEncryption**) to the **HLS** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="23029-169">Bir AssetDeliveryPolicy oluştururken belirtebilirsiniz değerleri hakkında bilgi için bkz: [AssetDeliveryPolicy tanımlarken kullanılan türleri](#types) bölümü.</span><span class="sxs-lookup"><span data-stu-id="23029-169">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="23029-170">İsteği:</span><span class="sxs-lookup"><span data-stu-id="23029-170">Request:</span></span>

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


<span data-ttu-id="23029-171">Yanıtı:</span><span class="sxs-lookup"><span data-stu-id="23029-171">Response:</span></span>

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


### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="23029-172">Varlık teslim ilkesini bağlantı varlığı</span><span class="sxs-lookup"><span data-stu-id="23029-172">Link asset with asset delivery policy</span></span>
<span data-ttu-id="23029-173">Bkz: [varlık teslim ilkesini bağlantı varlığı](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="23029-173">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="23029-174">DynamicCommonEncryption varlık teslim ilkesini</span><span class="sxs-lookup"><span data-stu-id="23029-174">DynamicCommonEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-the-commonencryption-type-and-link-it-to-the-asset"></a><span data-ttu-id="23029-175">CommonEncryption tür içerik anahtarı oluşturup varlık için Bağla</span><span class="sxs-lookup"><span data-stu-id="23029-175">Create content key of the CommonEncryption type and link it to the asset</span></span>
<span data-ttu-id="23029-176">DynamicCommonEncryption teslim İlkesi belirtirken, varlık CommonEncryption türü için bir içerik anahtarı bağlamak emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="23029-176">When specifying DynamicCommonEncryption delivery policy, you need to make sure to link your asset to a content key of the CommonEncryption type.</span></span> <span data-ttu-id="23029-177">Daha fazla bilgi için bkz: [bir içerik anahtarı oluşturma](media-services-rest-create-contentkey.md)).</span><span class="sxs-lookup"><span data-stu-id="23029-177">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <a name="get-delivery-url"></a><span data-ttu-id="23029-178">Teslim URL'sini alma</span><span class="sxs-lookup"><span data-stu-id="23029-178">Get Delivery URL</span></span>
<span data-ttu-id="23029-179">Önceki adımda oluşturduğunuz içerik anahtarı PlayReady teslim yöntemini teslim URL'sini alma.</span><span class="sxs-lookup"><span data-stu-id="23029-179">Get the delivery URL for the PlayReady delivery method of the content key created in the previous step.</span></span> <span data-ttu-id="23029-180">Bir istemci döndürülen URL PlayReady lisans korumalı içeriği kayıttan yürütme sırada istemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="23029-180">A client uses the returned URL to request a PlayReady license in order to playback the protected content.</span></span> <span data-ttu-id="23029-181">Daha fazla bilgi için bkz: [alma teslim URL](#get_delivery_url).</span><span class="sxs-lookup"><span data-stu-id="23029-181">For more information, see [Get Delivery URL](#get_delivery_url).</span></span>

### <a name="create-asset-delivery-policy"></a><span data-ttu-id="23029-182">Varlık teslim ilkesini oluşturma</span><span class="sxs-lookup"><span data-stu-id="23029-182">Create asset delivery policy</span></span>
<span data-ttu-id="23029-183">Aşağıdaki HTTP isteği oluşturur **AssetDeliveryPolicy** dinamik ortak şifreleme uygulamak için yapılandırılmış (**DynamicCommonEncryption**) için **kesintisiz akış** Protokolü (Bu örnekte, diğer protokolleri akışla aktarılması engellenir).</span><span class="sxs-lookup"><span data-stu-id="23029-183">The following HTTP request creates the **AssetDeliveryPolicy** that is configured to apply dynamic common encryption (**DynamicCommonEncryption**) to the **Smooth Streaming** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="23029-184">Bir AssetDeliveryPolicy oluştururken belirtebilirsiniz değerleri hakkında bilgi için bkz: [AssetDeliveryPolicy tanımlarken kullanılan türleri](#types) bölümü.</span><span class="sxs-lookup"><span data-stu-id="23029-184">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="23029-185">İsteği:</span><span class="sxs-lookup"><span data-stu-id="23029-185">Request:</span></span>

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


<span data-ttu-id="23029-186">Widevine DRM kullanarak içeriğinizi korumak istiyorsanız, (7 değeri olan) WidevineLicenseAcquisitionUrl kullanılacak AssetDeliveryConfiguration değerlerini güncelleştirin ve bir lisans teslimat hizmeti URL'sini belirtin.</span><span class="sxs-lookup"><span data-stu-id="23029-186">If you want to protect your content using Widevine DRM, update the AssetDeliveryConfiguration values to use WidevineLicenseAcquisitionUrl (which has the value of 7) and specify the URL of a license delivery service.</span></span> <span data-ttu-id="23029-187">Widevine lisansları teslim yardımcı olmak için şu AMS ortaklarını kullanabilirsiniz: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="23029-187">You can use the following AMS partners to help you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="23029-188">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="23029-188">For example:</span></span> 

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":2,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":7,\"Value\":\"https:\\/\\/example.net\/WidevineLicenseAcquisition\/"}]"}

> [!NOTE]
> <span data-ttu-id="23029-189">Widevine ile şifrelerken yalnızca tire kullanarak teslim etmek mümkün olacaktır.</span><span class="sxs-lookup"><span data-stu-id="23029-189">When encrypting with Widevine, you would only be able to deliver using DASH.</span></span> <span data-ttu-id="23029-190">Varlık teslim Protokolü tire (2) belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="23029-190">Make sure to specify DASH (2) in the asset delivery protocol.</span></span>
> 
> 

### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="23029-191">Varlık teslim ilkesini bağlantı varlığı</span><span class="sxs-lookup"><span data-stu-id="23029-191">Link asset with asset delivery policy</span></span>
<span data-ttu-id="23029-192">Bkz: [varlık teslim ilkesini bağlantı varlığı](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="23029-192">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <span data-ttu-id="23029-193"><a id="types"></a>AssetDeliveryPolicy tanımlarken kullanılan türleri</span><span class="sxs-lookup"><span data-stu-id="23029-193"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <a name="assetdeliveryprotocol"></a><span data-ttu-id="23029-194">AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="23029-194">AssetDeliveryProtocol</span></span>

<span data-ttu-id="23029-195">Aşağıdaki liste, varlık teslim protokolü için ayarlayabileceğiniz değerler açıklar.</span><span class="sxs-lookup"><span data-stu-id="23029-195">The following enum describes values you can set for the asset delivery protocol.</span></span>

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

### <a name="assetdeliverypolicytype"></a><span data-ttu-id="23029-196">AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="23029-196">AssetDeliveryPolicyType</span></span>

<span data-ttu-id="23029-197">Aşağıdaki liste varlık teslim İlkesi türü için ayarlayabileceğiniz değerler açıklar.</span><span class="sxs-lookup"><span data-stu-id="23029-197">The following enum describes values you can set for the asset delivery policy type.</span></span>  

    public enum AssetDeliveryPolicyType
    {
        /// <summary>
        /// Delivery Policy Type not set.  An invalid value.
        /// </summary>
        None,

        /// <summary>
        /// The Asset should not be delivered via this AssetDeliveryProtocol. 
        /// </summary>
        Blocked, 

        /// <summary>
        /// Do not apply dynamic encryption to the asset.
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

### <a name="contentkeydeliverytype"></a><span data-ttu-id="23029-198">ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="23029-198">ContentKeyDeliveryType</span></span>

<span data-ttu-id="23029-199">Aşağıdaki liste, içerik anahtarının istemciye teslim yöntemini yapılandırmak için kullanabileceğiniz değerleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="23029-199">The following enum describes values you can use to configure the delivery method of the content key to the client.</span></span>
    
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


### <a name="assetdeliverypolicyconfigurationkey"></a><span data-ttu-id="23029-200">AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="23029-200">AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="23029-201">Aşağıdaki liste, belirli bir yapılandırma için bir varlık teslim ilkesini almak için kullanılan anahtarları yapılandırmak için ayarlayabilirsiniz değerleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="23029-201">The following enum describes values you can set to configure keys used to get specific configuration for an asset delivery policy.</span></span>

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
        /// The initialization vector to use for envelope encryption in Base64 format.
        /// </summary>
        EnvelopeEncryptionIVAsBase64,

        /// <summary>
        /// The PlayReady License Acquisition Url to use for common encryption.
        /// </summary>
        PlayReadyLicenseAcquisitionUrl,

        /// <summary>
        /// The PlayReady Custom Attributes to add to the PlayReady Content Header
        /// </summary>
        PlayReadyCustomAttributes,

        /// <summary>
        /// The initialization vector to use for envelope encryption.
        /// </summary>
        EnvelopeEncryptionIV,

        /// <summary>
        /// Widevine DRM acquisition url
        /// </summary>
        WidevineLicenseAcquisitionUrl
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="23029-202">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="23029-202">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="23029-203">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="23029-203">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

