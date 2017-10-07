---
title: ".NET SDK'sı aaaConfigure varlık teslim ilkeleri | Microsoft Docs"
description: "Bu konuda gösterilmektedir nasıl Azure Media Services .NET SDK'sı ile tooconfigure farklı varlık teslim ilkeleri."
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
ms.openlocfilehash: a6f2644d639cd36d4cdc269b6f01fd4acdf7160b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-asset-delivery-policies-with-net-sdk"></a><span data-ttu-id="ccd44-103">.NET SDK'sı ile varlık teslim ilkeleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ccd44-103">Configure asset delivery policies with .NET SDK</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a><span data-ttu-id="ccd44-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="ccd44-104">Overview</span></span>
<span data-ttu-id="ccd44-105">Şifrelenmiş toodelivery varlıklar planlıyorsanız, hello birini hello medya Hizmetleri içerik teslim iş akışı varlıklar için teslim ilkelerini yapılandırma adımları.</span><span class="sxs-lookup"><span data-stu-id="ccd44-105">If you plan toodelivery encrypted assets, one of hello steps in hello Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="ccd44-106">Merhaba varlık teslim ilkesini Media Services nasıl teslim, varlık toobe için istediğinizi söyler: toodynamically istediğiniz olup olmadığına bakılmaksızın hangi akış protokolüne Varlığınızı dinamik olarak (örneğin, MPEG DASH, HLS, kesintisiz akış veya tümü için), paketlenmiş Varlığınızı şifrelemek ve nasıl (Zarf veya ortak şifreleme).</span><span class="sxs-lookup"><span data-stu-id="ccd44-106">hello asset delivery policy tells Media Services how you want for your asset toobe delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want toodynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="ccd44-107">Bu konuda neden ve nasıl anlatılmaktadır toocreate ve varlık teslim ilkeleri yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ccd44-107">This topic discusses why and how toocreate and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="ccd44-108">AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu.</span><span class="sxs-lookup"><span data-stu-id="ccd44-108">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="ccd44-109">İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu.</span><span class="sxs-lookup"><span data-stu-id="ccd44-109">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
>
><span data-ttu-id="ccd44-110">Ayrıca, toobe mümkün toouse dinamik paketleme ve dinamik şifreleme Varlığınızı içermelidir Uyarlamalı bit hızlı MP4s veya uyarlamalı bit hızlı kesintisiz akış dosyaları kümesidir.</span><span class="sxs-lookup"><span data-stu-id="ccd44-110">Also, toobe able toouse dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>


<span data-ttu-id="ccd44-111">Farklı ilkeleri toohello uygulayabilir aynı varlık.</span><span class="sxs-lookup"><span data-stu-id="ccd44-111">You could apply different policies toohello same asset.</span></span> <span data-ttu-id="ccd44-112">Örneğin, PlayReady şifreleme tooSmooth akış ve AES zarfı şifreleme tooMPEG uygulayabilir DASH ve HLS.</span><span class="sxs-lookup"><span data-stu-id="ccd44-112">For example, you could apply PlayReady encryption tooSmooth Streaming and AES Envelope encryption tooMPEG DASH and HLS.</span></span> <span data-ttu-id="ccd44-113">Bir teslim ilkesinde tanımlanmayan tüm protokollerin (örneğin, yalnızca hello protokol olarak HLS belirten tek bir ilke ekliyorsunuz) akışla aktarılması engellenir.</span><span class="sxs-lookup"><span data-stu-id="ccd44-113">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="ccd44-114">Merhaba özel durum toothis hiç tanımlanmış hiçbir varlık teslim ilkesini varsa ' dir.</span><span class="sxs-lookup"><span data-stu-id="ccd44-114">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="ccd44-115">Ardından, tüm protokoller hello Temizle izin verilir.</span><span class="sxs-lookup"><span data-stu-id="ccd44-115">Then, all protocols will be allowed in hello clear.</span></span>

<span data-ttu-id="ccd44-116">Toodeliver depolama şifrelenmiş varlık isterseniz hello varlığın teslim ilkesini yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ccd44-116">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="ccd44-117">Varlığınızı akışı önce sunucu kaldırır hello depolama şifrelemesi ve akışlar hello kullanarak içeriğinizi akış hello teslim ilkesini belirtilen.</span><span class="sxs-lookup"><span data-stu-id="ccd44-117">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="ccd44-118">Örneğin, toodeliver Varlığınızı Gelişmiş Şifreleme Standardı (AES) Zarf şifreleme anahtarıyla şifrelenir, çok hello ilke türünü ayarlayın**DynamicEnvelopeEncryption**.</span><span class="sxs-lookup"><span data-stu-id="ccd44-118">For example, toodeliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set hello policy type too**DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="ccd44-119">tooremove depolama şifreleme ve hello Temizle, akış hello varlığı ayarlamak hello ilke türü çok**NoDynamicEncryption**.</span><span class="sxs-lookup"><span data-stu-id="ccd44-119">tooremove storage encryption and stream hello asset in hello clear, set hello policy type too**NoDynamicEncryption**.</span></span> <span data-ttu-id="ccd44-120">Bu ilke türleri tooconfigure nasıl izleyin Göster örnekleri.</span><span class="sxs-lookup"><span data-stu-id="ccd44-120">Examples that show how tooconfigure these policy types follow.</span></span>

<span data-ttu-id="ccd44-121">Hello varlık teslim ilkesini nasıl yapılandırdığınıza bağlı mümkün toodynamically paketi, dinamik olarak şifrelemek ve akış akış protokolleri aşağıdaki hello: kesintisiz akış, HLS ve MPEG DASH akışları.</span><span class="sxs-lookup"><span data-stu-id="ccd44-121">Depending on how you configure hello asset delivery policy you would be able toodynamically package, dynamically encrypt, and stream hello following streaming protocols: Smooth Streaming, HLS, and MPEG DASH streams.</span></span>

<span data-ttu-id="ccd44-122">Merhaba aşağıdaki liste hello biçimleri toostream kesintisiz, HLS ve tire kullanın gösterir.</span><span class="sxs-lookup"><span data-stu-id="ccd44-122">hello following list shows hello formats that you use toostream Smooth, HLS, and DASH.</span></span>

<span data-ttu-id="ccd44-123">Kesintisiz akış:</span><span class="sxs-lookup"><span data-stu-id="ccd44-123">Smooth Streaming:</span></span>

<span data-ttu-id="ccd44-124">{akış uç noktası adı-media services hesabı adı}.streaming.mediaservices.windows.net/{konum kimliği}/{dosya adı}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="ccd44-124">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="ccd44-125">HLS:</span><span class="sxs-lookup"><span data-stu-id="ccd44-125">HLS:</span></span>

<span data-ttu-id="ccd44-126">{uç nokta adı media services hesabı name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl) akış</span><span class="sxs-lookup"><span data-stu-id="ccd44-126">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="ccd44-127">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="ccd44-127">MPEG DASH</span></span>

<span data-ttu-id="ccd44-128">{uç nokta adı media services hesabı name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf) akış</span><span class="sxs-lookup"><span data-stu-id="ccd44-128">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


## <a name="considerations"></a><span data-ttu-id="ccd44-129">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="ccd44-129">Considerations</span></span>
* <span data-ttu-id="ccd44-130">Bu varlık için bir (akış) OnDemand Bulucu bulunmakla birlikte bir varlıkla ilişkilendirilen AssetDeliveryPolicy silemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="ccd44-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="ccd44-131">Merhaba tooremove hello hello varlık ilkesinden hello İlkesi silmeden önce önerilir.</span><span class="sxs-lookup"><span data-stu-id="ccd44-131">hello recommendation is tooremove hello policy from hello asset before deleting hello policy.</span></span>
* <span data-ttu-id="ccd44-132">Hiçbir varlık teslim ilkesini ayarlandığında akış Bulucusu bir depolama şifrelenmiş varlık oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="ccd44-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="ccd44-133">Merhaba varlık şifrelenmiş depolama değilse, hello sistem, bir varlık teslim ilkesini olmadan temizleyin hello Bulucu ve akış hello varlık oluşturmak olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="ccd44-133">If hello Asset isn’t storage encrypted, hello system will let you create a locator and stream hello asset in hello clear without an asset delivery policy.</span></span>
* <span data-ttu-id="ccd44-134">Tek bir varlık ile ilişkili birden çok varlık teslim ilkeleri olabilir ancak yalnızca tek yönlü toohandle verilen AssetDeliveryProtocol belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ccd44-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way toohandle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="ccd44-135">Bir istemci bir kesintisiz akış bir istekte bulunduğunda hello sistem hangisinin bilmediğinden, bir hatayla sonuçlanır hello AssetDeliveryProtocol.SmoothStreaming protokolü belirtmek toolink iki teslim İlkesi çalışırsanız anlamına tooapply istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="ccd44-135">Meaning if you try toolink two delivery policies that specify hello AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because hello system does not know which one you want it tooapply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="ccd44-136">Bir varlığı ile var olan bir akış Bulucu varsa (Merhaba varlık varolan bir ilkeden bağlantısını, veya hello varlık ile ilişkili bir teslim ilkesini güncelleştirmek) yeni bir ilke toohello varlık bağlayamazsınız.</span><span class="sxs-lookup"><span data-stu-id="ccd44-136">If you have an asset with an existing streaming locator, you cannot link a new policy toohello asset (you can either unlink an existing policy from hello asset, or update a delivery policy associated with hello asset).</span></span>  <span data-ttu-id="ccd44-137">İlk tooremove hello akış Bulucusu sahip hello ilkeleri ayarlamak ve akış Bulucu hello yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ccd44-137">You first have tooremove hello streaming locator, adjust hello policies, and then re-create hello streaming locator.</span></span>  <span data-ttu-id="ccd44-138">İçerik hello Menşe veya bir aşağı akış CDN tarafından önbelleğe bu yana, istemciler için sorunlara neden olmaz Bulucu ancak Akış hello yeniden oluşturduğunuzda aynı locatorId emin olmalısınız hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ccd44-138">You can use hello same locatorId when you recreate hello streaming locator but you should ensure that won’t cause issues for clients since content can be cached by hello origin or a downstream CDN.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="ccd44-139">Clear varlık teslim ilkesini</span><span class="sxs-lookup"><span data-stu-id="ccd44-139">Clear asset delivery policy</span></span>

<span data-ttu-id="ccd44-140">Merhaba aşağıdaki **ConfigureClearAssetDeliveryPolicy** toonot dinamik şifreleme uygulanır ve aşağıdaki hello hiçbirinde toodeliver hello akış protokolleri yöntemini belirtir: MPEG DASH, HLS ve kesintisiz akış protokollerini.</span><span class="sxs-lookup"><span data-stu-id="ccd44-140">hello following **ConfigureClearAssetDeliveryPolicy** method specifies toonot apply dynamic encryption and toodeliver hello stream in any of hello following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> <span data-ttu-id="ccd44-141">Bu ilke tooyour şifrelenmiş depolama varlıklar tooapply isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ccd44-141">You might want tooapply this policy tooyour storage encrypted assets.</span></span>

<span data-ttu-id="ccd44-142">Merhaba, değerleri bilgi bir AssetDeliveryPolicy oluştururken belirtebilirsiniz için bkz: [AssetDeliveryPolicy tanımlarken kullanılan türleri](#types) bölümü.</span><span class="sxs-lookup"><span data-stu-id="ccd44-142">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="ccd44-143">DynamicCommonEncryption varlık teslim ilkesini</span><span class="sxs-lookup"><span data-stu-id="ccd44-143">DynamicCommonEncryption asset delivery policy</span></span>

<span data-ttu-id="ccd44-144">Merhaba aşağıdaki **CreateAssetDeliveryPolicy** yöntemi oluşturur hello **AssetDeliveryPolicy** diğer bir deyişle yapılandırılmış tooapply dinamik ortak şifreleme (**DynamicCommonEncryption**) tooa kesintisiz akış protokolüne (diğer protokoller akışla aktarılması engellenir).</span><span class="sxs-lookup"><span data-stu-id="ccd44-144">hello following **CreateAssetDeliveryPolicy** method creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic common encryption (**DynamicCommonEncryption**) tooa smooth streaming protocol (other protocols will be blocked from streaming).</span></span> <span data-ttu-id="ccd44-145">Merhaba yöntemi iki parametre alır: **varlık** (tooapply hello teslim ilkesini istediğiniz varlık toowhich hello) ve **IContentKey** (Merhaba hello içerik anahtarı **CommonEncryption**türü, daha fazla bilgi için bkz: [bir içerik anahtarı oluşturma](media-services-dotnet-create-contentkey.md#common_contentkey)).</span><span class="sxs-lookup"><span data-stu-id="ccd44-145">hello method takes two parameters : **Asset** (hello asset toowhich you want tooapply hello delivery policy) and **IContentKey** (hello content key of hello **CommonEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#common_contentkey)).</span></span>

<span data-ttu-id="ccd44-146">Merhaba, değerleri bilgi bir AssetDeliveryPolicy oluştururken belirtebilirsiniz için bkz: [AssetDeliveryPolicy tanımlarken kullanılan türleri](#types) bölümü.</span><span class="sxs-lookup"><span data-stu-id="ccd44-146">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

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
    
            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
    
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
                assetDeliveryPolicy.AssetDeliveryPolicyType);
     }

<span data-ttu-id="ccd44-147">Azure Media Services de tooadd Widevine şifrelemeyi etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="ccd44-147">Azure Media Services also enables you tooadd Widevine encryption.</span></span> <span data-ttu-id="ccd44-148">Merhaba aşağıdaki örnek PlayReady ve Widevine toohello varlık teslim ilkesini eklenmekte olan gösterir.</span><span class="sxs-lookup"><span data-stu-id="ccd44-148">hello following example demonstrates both PlayReady and Widevine being added toohello asset delivery policy.</span></span>

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        // Get hello PlayReady license service URL.
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);


        // GetKeyDeliveryUrl for Widevine attaches hello KID toohello URL.
        // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
        // hello WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption 
        // tooappend /? KID =< keyId > toohello end of hello url when creating hello manifest.
        // As a result Widevine license acquisition URL will have KID appended twice, 
        // so we need tooremove hello KID that in hello URL when we call GetKeyDeliveryUrl.

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


        // Add AssetDelivery Policy toohello asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

    }

> [!NOTE]
> <span data-ttu-id="ccd44-149">Widevine ile şifrelerken tire kullanarak mümkün toodeliver yalnızca olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ccd44-149">When encrypting with Widevine, you would only be able toodeliver using DASH.</span></span> <span data-ttu-id="ccd44-150">Emin toospecify tire hello varlık teslim Protokolü olun.</span><span class="sxs-lookup"><span data-stu-id="ccd44-150">Make sure toospecify DASH in hello asset delivery protocol.</span></span>
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="ccd44-151">DynamicEnvelopeEncryption varlık teslim ilkesini</span><span class="sxs-lookup"><span data-stu-id="ccd44-151">DynamicEnvelopeEncryption asset delivery policy</span></span>
<span data-ttu-id="ccd44-152">Merhaba aşağıdaki **CreateAssetDeliveryPolicy** yöntemi oluşturur hello **AssetDeliveryPolicy** diğer bir deyişle yapılandırılmış tooapply dinamik Zarf şifreleme (**DynamicEnvelopeEncryption** ) tooSmooth akış, HLS ve tire protokollerini (siz karar verirseniz, toonot belirtin bazı protokoller, akışla aktarılması engellenir).</span><span class="sxs-lookup"><span data-stu-id="ccd44-152">hello following **CreateAssetDeliveryPolicy** method creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic envelope encryption (**DynamicEnvelopeEncryption**) tooSmooth Streaming, HLS, and DASH protocols (if you decide toonot specify some protocols, they will be blocked from streaming).</span></span> <span data-ttu-id="ccd44-153">Merhaba yöntemi iki parametre alır: **varlık** (tooapply hello teslim ilkesini istediğiniz varlık toowhich hello) ve **IContentKey** (Merhaba hello içerik anahtarı **EnvelopeEncryption**türü, daha fazla bilgi için bkz: [bir içerik anahtarı oluşturma](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span><span class="sxs-lookup"><span data-stu-id="ccd44-153">hello method takes two parameters : **Asset** (hello asset toowhich you want tooapply hello delivery policy) and **IContentKey** (hello content key of hello **EnvelopeEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span></span>

<span data-ttu-id="ccd44-154">Merhaba, değerleri bilgi bir AssetDeliveryPolicy oluştururken belirtebilirsiniz için bkz: [AssetDeliveryPolicy tanımlarken kullanılan türleri](#types) bölümü.</span><span class="sxs-lookup"><span data-stu-id="ccd44-154">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

    private static void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {

        //  Get hello Key Delivery Base Url by removing hello Query parameter.  hello Dynamic Encryption service will
        //  automatically add hello correct key identifier toohello url when it generates hello Envelope encrypted content
        //  manifest.  Omitting hello IV will also cause hello Dynamice Encryption service toogenerate a deterministic
        //  IV for hello content automatically.  By using hello EnvelopeBaseKeyAcquisitionUrl and omitting hello IV, this
        //  allows hello AssetDelivery policy toobe reused by more than one asset.
        //
        Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);
        UriBuilder uriBuilder = new UriBuilder(keyAcquisitionUri);
        uriBuilder.Query = String.Empty;
        keyAcquisitionUri = uriBuilder.Uri;

        // hello following policy configuration specifies: 
        //   key url that will have KID=<Guid> appended toohello envelope and
        //   hello Initialization Vector (IV) toouse for hello envelope encryption.
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

        // Add AssetDelivery Policy toohello asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        Console.WriteLine();
        Console.WriteLine("Adding Asset Delivery Policy: " + assetDeliveryPolicy.AssetDeliveryPolicyType);
    }


## <span data-ttu-id="ccd44-155"><a id="types"></a>AssetDeliveryPolicy tanımlarken kullanılan türleri</span><span class="sxs-lookup"><span data-stu-id="ccd44-155"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <span data-ttu-id="ccd44-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="ccd44-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span></span>

<span data-ttu-id="ccd44-157">Merhaba aşağıdaki enum hello varlık teslim protokolü için ayarlayabileceğiniz değerler açıklar.</span><span class="sxs-lookup"><span data-stu-id="ccd44-157">hello following enum describes values you can set for hello asset delivery protocol.</span></span>

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

### <span data-ttu-id="ccd44-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="ccd44-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span></span>

<span data-ttu-id="ccd44-159">Merhaba aşağıdaki enum hello varlık teslim İlkesi türü için ayarlayabileceğiniz değerler açıklar.</span><span class="sxs-lookup"><span data-stu-id="ccd44-159">hello following enum describes values you can set for hello asset delivery policy type.</span></span>  

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

### <span data-ttu-id="ccd44-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="ccd44-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>

<span data-ttu-id="ccd44-161">Merhaba aşağıdaki enum değerleri hello içerik anahtar toohello istemci tooconfigure hello teslim yöntemini kullanabilirsiniz açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ccd44-161">hello following enum describes values you can use tooconfigure hello delivery method of hello content key toohello client.</span></span>
    
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

### <span data-ttu-id="ccd44-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="ccd44-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="ccd44-163">Enum aşağıdaki hello tooconfigure kullanılan anahtarları tooget belirli yapılandırma için bir varlık teslim ilkesini ayarlayabilirsiniz değerleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ccd44-163">hello following enum describes values you can set tooconfigure keys used tooget specific configuration for an asset delivery policy.</span></span>

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="ccd44-164">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="ccd44-164">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ccd44-165">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="ccd44-165">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

