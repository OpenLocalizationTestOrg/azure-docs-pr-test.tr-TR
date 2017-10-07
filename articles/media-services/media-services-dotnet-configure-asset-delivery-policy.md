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
# <a name="configure-asset-delivery-policies-with-net-sdk"></a>.NET SDK'sı ile varlık teslim ilkeleri yapılandırma
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a>Genel Bakış
Şifrelenmiş toodelivery varlıklar planlıyorsanız, hello birini hello medya Hizmetleri içerik teslim iş akışı varlıklar için teslim ilkelerini yapılandırma adımları. Merhaba varlık teslim ilkesini Media Services nasıl teslim, varlık toobe için istediğinizi söyler: toodynamically istediğiniz olup olmadığına bakılmaksızın hangi akış protokolüne Varlığınızı dinamik olarak (örneğin, MPEG DASH, HLS, kesintisiz akış veya tümü için), paketlenmiş Varlığınızı şifrelemek ve nasıl (Zarf veya ortak şifreleme).

Bu konuda neden ve nasıl anlatılmaktadır toocreate ve varlık teslim ilkeleri yapılandırın.

>[!NOTE]
>AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu. İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu. 
>
>Ayrıca, toobe mümkün toouse dinamik paketleme ve dinamik şifreleme Varlığınızı içermelidir Uyarlamalı bit hızlı MP4s veya uyarlamalı bit hızlı kesintisiz akış dosyaları kümesidir.


Farklı ilkeleri toohello uygulayabilir aynı varlık. Örneğin, PlayReady şifreleme tooSmooth akış ve AES zarfı şifreleme tooMPEG uygulayabilir DASH ve HLS. Bir teslim ilkesinde tanımlanmayan tüm protokollerin (örneğin, yalnızca hello protokol olarak HLS belirten tek bir ilke ekliyorsunuz) akışla aktarılması engellenir. Merhaba özel durum toothis hiç tanımlanmış hiçbir varlık teslim ilkesini varsa ' dir. Ardından, tüm protokoller hello Temizle izin verilir.

Toodeliver depolama şifrelenmiş varlık isterseniz hello varlığın teslim ilkesini yapılandırmanız gerekir. Varlığınızı akışı önce sunucu kaldırır hello depolama şifrelemesi ve akışlar hello kullanarak içeriğinizi akış hello teslim ilkesini belirtilen. Örneğin, toodeliver Varlığınızı Gelişmiş Şifreleme Standardı (AES) Zarf şifreleme anahtarıyla şifrelenir, çok hello ilke türünü ayarlayın**DynamicEnvelopeEncryption**. tooremove depolama şifreleme ve hello Temizle, akış hello varlığı ayarlamak hello ilke türü çok**NoDynamicEncryption**. Bu ilke türleri tooconfigure nasıl izleyin Göster örnekleri.

Hello varlık teslim ilkesini nasıl yapılandırdığınıza bağlı mümkün toodynamically paketi, dinamik olarak şifrelemek ve akış akış protokolleri aşağıdaki hello: kesintisiz akış, HLS ve MPEG DASH akışları.

Merhaba aşağıdaki liste hello biçimleri toostream kesintisiz, HLS ve tire kullanın gösterir.

Kesintisiz akış:

{akış uç noktası adı-media services hesabı adı}.streaming.mediaservices.windows.net/{konum kimliği}/{dosya adı}.ism/Manifest

HLS:

{uç nokta adı media services hesabı name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl) akış

MPEG DASH

{uç nokta adı media services hesabı name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf) akış


## <a name="considerations"></a>Dikkat edilmesi gerekenler
* Bu varlık için bir (akış) OnDemand Bulucu bulunmakla birlikte bir varlıkla ilişkilendirilen AssetDeliveryPolicy silemezsiniz. Merhaba tooremove hello hello varlık ilkesinden hello İlkesi silmeden önce önerilir.
* Hiçbir varlık teslim ilkesini ayarlandığında akış Bulucusu bir depolama şifrelenmiş varlık oluşturulamıyor.  Merhaba varlık şifrelenmiş depolama değilse, hello sistem, bir varlık teslim ilkesini olmadan temizleyin hello Bulucu ve akış hello varlık oluşturmak olanak tanır.
* Tek bir varlık ile ilişkili birden çok varlık teslim ilkeleri olabilir ancak yalnızca tek yönlü toohandle verilen AssetDeliveryProtocol belirtebilirsiniz.  Bir istemci bir kesintisiz akış bir istekte bulunduğunda hello sistem hangisinin bilmediğinden, bir hatayla sonuçlanır hello AssetDeliveryProtocol.SmoothStreaming protokolü belirtmek toolink iki teslim İlkesi çalışırsanız anlamına tooapply istediğiniz.
* Bir varlığı ile var olan bir akış Bulucu varsa (Merhaba varlık varolan bir ilkeden bağlantısını, veya hello varlık ile ilişkili bir teslim ilkesini güncelleştirmek) yeni bir ilke toohello varlık bağlayamazsınız.  İlk tooremove hello akış Bulucusu sahip hello ilkeleri ayarlamak ve akış Bulucu hello yeniden oluşturun.  İçerik hello Menşe veya bir aşağı akış CDN tarafından önbelleğe bu yana, istemciler için sorunlara neden olmaz Bulucu ancak Akış hello yeniden oluşturduğunuzda aynı locatorId emin olmalısınız hello kullanabilirsiniz.

## <a name="clear-asset-delivery-policy"></a>Clear varlık teslim ilkesini

Merhaba aşağıdaki **ConfigureClearAssetDeliveryPolicy** toonot dinamik şifreleme uygulanır ve aşağıdaki hello hiçbirinde toodeliver hello akış protokolleri yöntemini belirtir: MPEG DASH, HLS ve kesintisiz akış protokollerini. Bu ilke tooyour şifrelenmiş depolama varlıklar tooapply isteyebilirsiniz.

Merhaba, değerleri bilgi bir AssetDeliveryPolicy oluştururken belirtebilirsiniz için bkz: [AssetDeliveryPolicy tanımlarken kullanılan türleri](#types) bölümü.

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a>DynamicCommonEncryption varlık teslim ilkesini

Merhaba aşağıdaki **CreateAssetDeliveryPolicy** yöntemi oluşturur hello **AssetDeliveryPolicy** diğer bir deyişle yapılandırılmış tooapply dinamik ortak şifreleme (**DynamicCommonEncryption**) tooa kesintisiz akış protokolüne (diğer protokoller akışla aktarılması engellenir). Merhaba yöntemi iki parametre alır: **varlık** (tooapply hello teslim ilkesini istediğiniz varlık toowhich hello) ve **IContentKey** (Merhaba hello içerik anahtarı **CommonEncryption**türü, daha fazla bilgi için bkz: [bir içerik anahtarı oluşturma](media-services-dotnet-create-contentkey.md#common_contentkey)).

Merhaba, değerleri bilgi bir AssetDeliveryPolicy oluştururken belirtebilirsiniz için bkz: [AssetDeliveryPolicy tanımlarken kullanılan türleri](#types) bölümü.

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

Azure Media Services de tooadd Widevine şifrelemeyi etkinleştirir. Merhaba aşağıdaki örnek PlayReady ve Widevine toohello varlık teslim ilkesini eklenmekte olan gösterir.

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
> Widevine ile şifrelerken tire kullanarak mümkün toodeliver yalnızca olacaktır. Emin toospecify tire hello varlık teslim Protokolü olun.
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a>DynamicEnvelopeEncryption varlık teslim ilkesini
Merhaba aşağıdaki **CreateAssetDeliveryPolicy** yöntemi oluşturur hello **AssetDeliveryPolicy** diğer bir deyişle yapılandırılmış tooapply dinamik Zarf şifreleme (**DynamicEnvelopeEncryption** ) tooSmooth akış, HLS ve tire protokollerini (siz karar verirseniz, toonot belirtin bazı protokoller, akışla aktarılması engellenir). Merhaba yöntemi iki parametre alır: **varlık** (tooapply hello teslim ilkesini istediğiniz varlık toowhich hello) ve **IContentKey** (Merhaba hello içerik anahtarı **EnvelopeEncryption**türü, daha fazla bilgi için bkz: [bir içerik anahtarı oluşturma](media-services-dotnet-create-contentkey.md#envelope_contentkey)).

Merhaba, değerleri bilgi bir AssetDeliveryPolicy oluştururken belirtebilirsiniz için bkz: [AssetDeliveryPolicy tanımlarken kullanılan türleri](#types) bölümü.   

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


## <a id="types"></a>AssetDeliveryPolicy tanımlarken kullanılan türleri

### <a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol

Merhaba aşağıdaki enum hello varlık teslim protokolü için ayarlayabileceğiniz değerler açıklar.

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

### <a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType

Merhaba aşağıdaki enum hello varlık teslim İlkesi türü için ayarlayabileceğiniz değerler açıklar.  

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

### <a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType

Merhaba aşağıdaki enum değerleri hello içerik anahtar toohello istemci tooconfigure hello teslim yöntemini kullanabilirsiniz açıklanmaktadır.
    
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

### <a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey

Enum aşağıdaki hello tooconfigure kullanılan anahtarları tooget belirli yapılandırma için bir varlık teslim ilkesini ayarlayabilirsiniz değerleri açıklanmaktadır.

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

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

