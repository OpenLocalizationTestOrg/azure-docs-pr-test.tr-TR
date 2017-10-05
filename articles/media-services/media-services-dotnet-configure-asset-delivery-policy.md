---
title: ".NET SDK'sı ile varlık teslim ilkeleri yapılandırma | Microsoft Docs"
description: "Bu konu Azure Media Services .NET SDK ile farklı varlık teslim ilkeleri yapılandırmak nasıl gösterir."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 3ec46f58-6cbb-4d49-bac6-1fd01a5a456b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/13/2017
ms.author: juliako;mingfeiy
ms.openlocfilehash: 282fd9e24dc147e31613469926128894d48366f4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-asset-delivery-policies-with-net-sdk"></a><span data-ttu-id="a61ef-103">.NET SDK'sı ile varlık teslim ilkeleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a61ef-103">Configure asset delivery policies with .NET SDK</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a><span data-ttu-id="a61ef-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="a61ef-104">Overview</span></span>
<span data-ttu-id="a61ef-105">Teslim şifrelenen varlıklarına planlıyorsanız, Media Services içerik teslim iş akışı'ndaki adımları birini varlıklar için teslim ilkeleri yapılandırıyor.</span><span class="sxs-lookup"><span data-stu-id="a61ef-105">If you plan to delivery encrypted assets, one of the steps in the Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="a61ef-106">Media Services, varlık teslim edilmesini istediğiniz varlık teslim ilkesini bildirir: hangi Akış Protokolü varlığınız dinamik olarak paketlenir (örneğin, MPEG DASH, HLS, kesintisiz akış veya tümü için), dinamik olarak Varlığınızı şifrelemek isteyip istemediğinizi ve nasıl içine (Zarf veya ortak şifreleme).</span><span class="sxs-lookup"><span data-stu-id="a61ef-106">The asset delivery policy tells Media Services how you want for your asset to be delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want to dynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="a61ef-107">Bu konuda ele alınmıştır neden ve nasıl oluşturulacağı ve varlık teslim ilkeleri yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a61ef-107">This topic discusses why and how to create and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="a61ef-108">AMS hesabınız oluşturulduğunda hesabınıza **Durdurulmuş** durumda bir **varsayılan** akış uç noktası eklenir.</span><span class="sxs-lookup"><span data-stu-id="a61ef-108">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="a61ef-109">İçerik akışını başlatmak ve dinamik paketleme ile dinamik şifrelemeden yararlanmak için içerik akışı yapmak istediğiniz akış uç noktasının **Çalışıyor** durumda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a61ef-109">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 
>
><span data-ttu-id="a61ef-110">Ayrıca, dinamik paketleme ve dinamik şifreleme kullanabilmek için varlığınız Uyarlamalı bit hızlı MP4s ya da Uyarlamalı bit hızlı kesintisiz akış dosyaları içermelidir.</span><span class="sxs-lookup"><span data-stu-id="a61ef-110">Also, to be able to use dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>


<span data-ttu-id="a61ef-111">Aynı varlık için farklı ilkeler uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a61ef-111">You could apply different policies to the same asset.</span></span> <span data-ttu-id="a61ef-112">Örneğin, MPEG DASH ve HLS için AES zarfı kesintisiz akış ve şifreleme için PlayReady şifreleme uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a61ef-112">For example, you could apply PlayReady encryption to Smooth Streaming and AES Envelope encryption to MPEG DASH and HLS.</span></span> <span data-ttu-id="a61ef-113">Herhangi bir teslim ilkesinde tanımlanmayan tüm protokollerin (örneğin, protokol olarak yalnızca HLS‘yi belirten tek bir ilke ekliyorsunuz) akışla aktarılması engellenir.</span><span class="sxs-lookup"><span data-stu-id="a61ef-113">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as the protocol) will be blocked from streaming.</span></span> <span data-ttu-id="a61ef-114">Bunun tek istisnası, hiçbir varlık teslim ilkesinin tanımlanmadığı durumdur.</span><span class="sxs-lookup"><span data-stu-id="a61ef-114">The exception to this is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="a61ef-115">Bu halde tüm protokollere açık bir şekilde izin verilir.</span><span class="sxs-lookup"><span data-stu-id="a61ef-115">Then, all protocols will be allowed in the clear.</span></span>

<span data-ttu-id="a61ef-116">Bir depolama şifrelenmiş varlık teslim etmek istiyorsanız, varlığın teslim ilkesini yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a61ef-116">If you want to deliver a storage encrypted asset, you must configure the asset’s delivery policy.</span></span> <span data-ttu-id="a61ef-117">Varlığınızı akışı önce akış sunucusu depolama şifreleme kaldırır ve belirtilen teslim ilkesini kullanarak içeriğinizi akışlarını.</span><span class="sxs-lookup"><span data-stu-id="a61ef-117">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy.</span></span> <span data-ttu-id="a61ef-118">Örneğin, Gelişmiş Şifreleme Standardı (AES) Zarf şifreleme anahtarıyla şifrelenir, varlık teslim etmek için ilke türünü ayarlamak **DynamicEnvelopeEncryption**.</span><span class="sxs-lookup"><span data-stu-id="a61ef-118">For example, to deliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set the policy type to **DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="a61ef-119">Depolama şifrelemesi kaldırmak ve varlık temiz akışını ilke türünü ayarlayın **NoDynamicEncryption**.</span><span class="sxs-lookup"><span data-stu-id="a61ef-119">To remove storage encryption and stream the asset in the clear, set the policy type to **NoDynamicEncryption**.</span></span> <span data-ttu-id="a61ef-120">Bu ilke türünü yapılandırmanız nasıl gösteren örnekler izleyin.</span><span class="sxs-lookup"><span data-stu-id="a61ef-120">Examples that show how to configure these policy types follow.</span></span>

<span data-ttu-id="a61ef-121">Varlık teslim ilkesini nasıl yapılandırdığınıza bağlı olarak, dinamik olarak paketini, dinamik olarak şifrelemek ve aşağıdaki akış protokolleri akışını gerçekleştirebilir: kesintisiz akış, HLS ve MPEG DASH akışları.</span><span class="sxs-lookup"><span data-stu-id="a61ef-121">Depending on how you configure the asset delivery policy you would be able to dynamically package, dynamically encrypt, and stream the following streaming protocols: Smooth Streaming, HLS, and MPEG DASH streams.</span></span>

<span data-ttu-id="a61ef-122">Aşağıdaki liste, kesintisiz, HLS ve tire akış için kullandığınız biçimleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="a61ef-122">The following list shows the formats that you use to stream Smooth, HLS, and DASH.</span></span>

<span data-ttu-id="a61ef-123">Kesintisiz akış:</span><span class="sxs-lookup"><span data-stu-id="a61ef-123">Smooth Streaming:</span></span>

<span data-ttu-id="a61ef-124">{akış uç noktası adı-media services hesabı adı}.streaming.mediaservices.windows.net/{konum kimliği}/{dosya adı}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="a61ef-124">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="a61ef-125">HLS:</span><span class="sxs-lookup"><span data-stu-id="a61ef-125">HLS:</span></span>

<span data-ttu-id="a61ef-126">{uç nokta adı media services hesabı name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl) akış</span><span class="sxs-lookup"><span data-stu-id="a61ef-126">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="a61ef-127">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="a61ef-127">MPEG DASH</span></span>

<span data-ttu-id="a61ef-128">{uç nokta adı media services hesabı name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf) akış</span><span class="sxs-lookup"><span data-stu-id="a61ef-128">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


## <a name="considerations"></a><span data-ttu-id="a61ef-129">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="a61ef-129">Considerations</span></span>
* <span data-ttu-id="a61ef-130">Bu varlık için bir (akış) OnDemand Bulucu bulunmakla birlikte bir varlıkla ilişkilendirilen AssetDeliveryPolicy silemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="a61ef-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="a61ef-131">İlke silmeden önce varlığından ilkesini kaldırmak için önerilir.</span><span class="sxs-lookup"><span data-stu-id="a61ef-131">The recommendation is to remove the policy from the asset before deleting the policy.</span></span>
* <span data-ttu-id="a61ef-132">Hiçbir varlık teslim ilkesini ayarlandığında akış Bulucusu bir depolama şifrelenmiş varlık oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="a61ef-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="a61ef-133">Varlık şifrelenmiş depolama yoksa, sistem, bir Bulucu oluşturmanız ve varlık bir varlık teslim ilkesini olmadan temiz akışını olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="a61ef-133">If the Asset isn’t storage encrypted, the system will let you create a locator and stream the asset in the clear without an asset delivery policy.</span></span>
* <span data-ttu-id="a61ef-134">Tek bir varlık ile ilişkili birden çok varlık teslim ilkeleri olabilir, ancak yalnızca belirli bir AssetDeliveryProtocol işlemek için bir yol belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a61ef-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way to handle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="a61ef-135">Sistem hangisinin, bir istemci bir kesintisiz akış bir istekte bulunduğunda uygulanacak bilmediğinden, bir hatayla sonuçlanır AssetDeliveryProtocol.SmoothStreaming protokolü belirtmek iki teslim ilkeleri bağlamaya çalışır anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="a61ef-135">Meaning if you try to link two delivery policies that specify the AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because the system does not know which one you want it to apply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="a61ef-136">Bir varlığı ile var olan bir akış Bulucu varsa varlık için yeni bir ilke bağlayamazsınız (, var olan bir varlık ilkesinden bağlantısını veya varlık ile ilişkili bir teslim ilkesini güncelleştirin).</span><span class="sxs-lookup"><span data-stu-id="a61ef-136">If you have an asset with an existing streaming locator, you cannot link a new policy to the asset (you can either unlink an existing policy from the asset, or update a delivery policy associated with the asset).</span></span>  <span data-ttu-id="a61ef-137">İlk bu akış Bulucusu kaldırmak, ilkeleri ayarlamak ve akış Bulucusu yeniden oluşturmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="a61ef-137">You first have to remove the streaming locator, adjust the policies, and then re-create the streaming locator.</span></span>  <span data-ttu-id="a61ef-138">Akış Bulucusu yeniden oluşturur ancak içerik kaynağı veya bir aşağı akış CDN tarafından önbelleğe beri sorunları istemciler için neden olmaz emin olmalısınız aynı locatorId kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a61ef-138">You can use the same locatorId when you recreate the streaming locator but you should ensure that won’t cause issues for clients since content can be cached by the origin or a downstream CDN.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="a61ef-139">Clear varlık teslim ilkesini</span><span class="sxs-lookup"><span data-stu-id="a61ef-139">Clear asset delivery policy</span></span>

<span data-ttu-id="a61ef-140">Aşağıdaki **ConfigureClearAssetDeliveryPolicy** dinamik şifreleme geçerli değil ve aşağıdaki protokollerden birini akışta teslim etmeyi yöntemini belirtir: MPEG DASH, HLS ve kesintisiz akış protokollerini.</span><span class="sxs-lookup"><span data-stu-id="a61ef-140">The following **ConfigureClearAssetDeliveryPolicy** method specifies to not apply dynamic encryption and to deliver the stream in any of the following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> <span data-ttu-id="a61ef-141">Bu ilke şifrelenmiş depolama varlıklarınızı uygulamak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a61ef-141">You might want to apply this policy to your storage encrypted assets.</span></span>

<span data-ttu-id="a61ef-142">Bir AssetDeliveryPolicy oluştururken belirtebilirsiniz değerleri hakkında bilgi için bkz: [AssetDeliveryPolicy tanımlarken kullanılan türleri](#types) bölümü.</span><span class="sxs-lookup"><span data-stu-id="a61ef-142">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="a61ef-143">DynamicCommonEncryption varlık teslim ilkesini</span><span class="sxs-lookup"><span data-stu-id="a61ef-143">DynamicCommonEncryption asset delivery policy</span></span>

<span data-ttu-id="a61ef-144">Aşağıdaki **CreateAssetDeliveryPolicy** yöntemi oluşturur **AssetDeliveryPolicy** dinamik ortak şifreleme uygulamak için yapılandırılmış (**DynamicCommonEncryption**) bir kesintisiz akış protokolüne (diğer protokoller engellenir akışla aktarılması).</span><span class="sxs-lookup"><span data-stu-id="a61ef-144">The following **CreateAssetDeliveryPolicy** method creates the **AssetDeliveryPolicy** that is configured to apply dynamic common encryption (**DynamicCommonEncryption**) to a smooth streaming protocol (other protocols will be blocked from streaming).</span></span> <span data-ttu-id="a61ef-145">Yöntemi iki parametre alır: **varlık** (varlık teslim ilkesini uygulamak istediğiniz) ve **IContentKey** (içerik anahtarı **CommonEncryption** türü için Daha fazla bilgi için bkz: [bir içerik anahtarı oluşturma](media-services-dotnet-create-contentkey.md#common_contentkey)).</span><span class="sxs-lookup"><span data-stu-id="a61ef-145">The method takes two parameters : **Asset** (the asset to which you want to apply the delivery policy) and **IContentKey** (the content key of the **CommonEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#common_contentkey)).</span></span>

<span data-ttu-id="a61ef-146">Bir AssetDeliveryPolicy oluştururken belirtebilirsiniz değerleri hakkında bilgi için bkz: [AssetDeliveryPolicy tanımlarken kullanılan türleri](#types) bölümü.</span><span class="sxs-lookup"><span data-stu-id="a61ef-146">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);
        
        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
                new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
            };
    
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                    "AssetDeliveryPolicy",
                AssetDeliveryPolicyType.DynamicCommonEncryption,
                AssetDeliveryProtocol.SmoothStreaming,
                assetDeliveryPolicyConfiguration);
    
            // Add AssetDelivery Policy to the asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
    
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
                assetDeliveryPolicy.AssetDeliveryPolicyType);
     }

<span data-ttu-id="a61ef-147">Azure Media Services Widevine şifreleme eklemenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="a61ef-147">Azure Media Services also enables you to add Widevine encryption.</span></span> <span data-ttu-id="a61ef-148">Aşağıdaki örnek, PlayReady ve Widevine için varlık teslim ilkesini eklenmekte olan gösterir.</span><span class="sxs-lookup"><span data-stu-id="a61ef-148">The following example demonstrates both PlayReady and Widevine being added to the asset delivery policy.</span></span>

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        // Get the PlayReady license service URL.
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);


        // GetKeyDeliveryUrl for Widevine attaches the KID to the URL.
        // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
        // The WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption 
        // to append /? KID =< keyId > to the end of the url when creating the manifest.
        // As a result Widevine license acquisition URL will have KID appended twice, 
        // so we need to remove the KID that in the URL when we call GetKeyDeliveryUrl.

        Uri widevineUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine);
        UriBuilder uriBuilder = new UriBuilder(widevineUrl);
        uriBuilder.Query = String.Empty;
        widevineUrl = uriBuilder.Uri;

        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
        {
            {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
            {AssetDeliveryPolicyConfigurationKey.WidevineLicenseAcquisitionUrl, widevineUrl.ToString()}

        };

        var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


        // Add AssetDelivery Policy to the asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

    }

> [!NOTE]
> <span data-ttu-id="a61ef-149">Widevine ile şifrelerken yalnızca tire kullanarak teslim etmek mümkün olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a61ef-149">When encrypting with Widevine, you would only be able to deliver using DASH.</span></span> <span data-ttu-id="a61ef-150">Varlık teslim Protokolü tire belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="a61ef-150">Make sure to specify DASH in the asset delivery protocol.</span></span>
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="a61ef-151">DynamicEnvelopeEncryption varlık teslim ilkesini</span><span class="sxs-lookup"><span data-stu-id="a61ef-151">DynamicEnvelopeEncryption asset delivery policy</span></span>
<span data-ttu-id="a61ef-152">Aşağıdaki **CreateAssetDeliveryPolicy** yöntemi oluşturur **AssetDeliveryPolicy** dinamik Zarf şifreleme uygulamak için yapılandırılmış (**DynamicEnvelopeEncryption**) Kesintisiz akış, HLS ve tire protokollere (bazı protokoller belirtmeyin karar verirseniz, bunlar akışla aktarılması engellenir).</span><span class="sxs-lookup"><span data-stu-id="a61ef-152">The following **CreateAssetDeliveryPolicy** method creates the **AssetDeliveryPolicy** that is configured to apply dynamic envelope encryption (**DynamicEnvelopeEncryption**) to Smooth Streaming, HLS, and DASH protocols (if you decide to not specify some protocols, they will be blocked from streaming).</span></span> <span data-ttu-id="a61ef-153">Yöntemi iki parametre alır: **varlık** (varlık teslim ilkesini uygulamak istediğiniz) ve **IContentKey** (içerik anahtarı **EnvelopeEncryption** türü Daha fazla bilgi için bkz: [bir içerik anahtarı oluşturma](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span><span class="sxs-lookup"><span data-stu-id="a61ef-153">The method takes two parameters : **Asset** (the asset to which you want to apply the delivery policy) and **IContentKey** (the content key of the **EnvelopeEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span></span>

<span data-ttu-id="a61ef-154">Bir AssetDeliveryPolicy oluştururken belirtebilirsiniz değerleri hakkında bilgi için bkz: [AssetDeliveryPolicy tanımlarken kullanılan türleri](#types) bölümü.</span><span class="sxs-lookup"><span data-stu-id="a61ef-154">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

    private static void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {

        //  Get the Key Delivery Base Url by removing the Query parameter.  The Dynamic Encryption service will
        //  automatically add the correct key identifier to the url when it generates the Envelope encrypted content
        //  manifest.  Omitting the IV will also cause the Dynamice Encryption service to generate a deterministic
        //  IV for the content automatically.  By using the EnvelopeBaseKeyAcquisitionUrl and omitting the IV, this
        //  allows the AssetDelivery policy to be reused by more than one asset.
        //
        Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);
        UriBuilder uriBuilder = new UriBuilder(keyAcquisitionUri);
        uriBuilder.Query = String.Empty;
        keyAcquisitionUri = uriBuilder.Uri;

        // The following policy configuration specifies: 
        //   key url that will have KID=<Guid> appended to the envelope and
        //   the Initialization Vector (IV) to use for the envelope encryption.
        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string> 
        {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeBaseKeyAcquisitionUrl, keyAcquisitionUri.ToString()},
        };

        IAssetDeliveryPolicy assetDeliveryPolicy =
            _context.AssetDeliveryPolicies.Create(
                        "AssetDeliveryPolicy",
                        AssetDeliveryPolicyType.DynamicEnvelopeEncryption,
                        AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.Dash,
                        assetDeliveryPolicyConfiguration);

        // Add AssetDelivery Policy to the asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        Console.WriteLine();
        Console.WriteLine("Adding Asset Delivery Policy: " + assetDeliveryPolicy.AssetDeliveryPolicyType);
    }


## <span data-ttu-id="a61ef-155"><a id="types"></a>AssetDeliveryPolicy tanımlarken kullanılan türleri</span><span class="sxs-lookup"><span data-stu-id="a61ef-155"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <span data-ttu-id="a61ef-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="a61ef-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span></span>

<span data-ttu-id="a61ef-157">Aşağıdaki liste, varlık teslim protokolü için ayarlayabileceğiniz değerler açıklar.</span><span class="sxs-lookup"><span data-stu-id="a61ef-157">The following enum describes values you can set for the asset delivery protocol.</span></span>

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

### <span data-ttu-id="a61ef-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="a61ef-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span></span>

<span data-ttu-id="a61ef-159">Aşağıdaki liste varlık teslim İlkesi türü için ayarlayabileceğiniz değerler açıklar.</span><span class="sxs-lookup"><span data-stu-id="a61ef-159">The following enum describes values you can set for the asset delivery policy type.</span></span>  

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

### <span data-ttu-id="a61ef-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="a61ef-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>

<span data-ttu-id="a61ef-161">Aşağıdaki liste, içerik anahtarının istemciye teslim yöntemini yapılandırmak için kullanabileceğiniz değerleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a61ef-161">The following enum describes values you can use to configure the delivery method of the content key to the client.</span></span>
    
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

### <span data-ttu-id="a61ef-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="a61ef-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="a61ef-163">Aşağıdaki liste, belirli bir yapılandırma için bir varlık teslim ilkesini almak için kullanılan anahtarları yapılandırmak için ayarlayabilirsiniz değerleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a61ef-163">The following enum describes values you can set to configure keys used to get specific configuration for an asset delivery policy.</span></span>

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="a61ef-164">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="a61ef-164">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a61ef-165">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="a61ef-165">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

