---
title: "Media Services .NET SDK kullanarak aaaConfigure içerik anahtarı yetkilendirme ilkesini | Microsoft Docs"
description: "Bilgi nasıl tooconfigure Media Services .NET SDK kullanarak bir içerik anahtarı için bir yetkilendirme ilkesi."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 1a0aedda-5b87-4436-8193-09fc2f14310c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;mingfeiy
ms.openlocfilehash: cfcbc5da9819bcec8b163fef183988a8beff9ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a>Dinamik şifreleme: içerik anahtarı yetkilendirme ilkesini yapılandırma
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a>Genel Bakış
Microsoft Azure Media Services sağlar toodeliver MPEG-DASH, kesintisiz akış ve HTTP canlı akış (HLS) akışlar Gelişmiş Şifreleme Standardı ((128-bit şifreleme anahtarları kullanılarak) AES ile) korumalı veya [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). AMS Ayrıca, Widevine DRM ile şifrelenmiş, toodeliver DASH akışları sağlar. PlayReady ve Widevine, ortak şifreleme (ISO/IEC 23001-7 CENC) belirtimi hello şifrelenir.

Medya Hizmetleri de sağlar bir **anahtarı/lisans teslimat hizmeti** hangi istemcilerin AES anahtarları elde edebilirsiniz veya PlayReady/Widevine lisansları tooplay hello şifrelenmiş içerik.

Bir varlık için Media Services tooencrypt istiyorsanız, tooassociate bir şifreleme anahtarı gerekir (**CommonEncryption** veya **EnvelopeEncryption**) hello varlık ile (açıklandığı gibi [burada](media-services-dotnet-create-contentkey.md)) ve ayrıca Yetkilendirme İlkeleri (Bu makalede anlatıldığı gibi) başlangıç anahtarı için yapılandırabilirsiniz.

Bir akış player tarafından istendiğinde Media Services belirtilen hello kullanan anahtar toodynamically AES veya DRM şifreleme kullanarak içeriğinizi şifreleyin. toodecrypt hello akış hello anahtar teslim hizmetinden hello anahtar hello player isteyin. tooget hello anahtar desteklemediğini hello kullanıcıdır toodecide yetkili, hello hizmet hello anahtar için belirtilen hello yetkilendirme ilkelerini değerlendirir.

Media Services, anahtar isteğinde bulunan kullanıcıların kimlik doğrulamasını yapmanın birden çok yöntemini destekler. Merhaba içerik anahtarı yetkilendirme ilkesini bir veya daha fazla yetkilendirme kısıtlamaları olabilir: **açmak** veya **belirteci** kısıtlama. Merhaba belirteç kısıtlamalı ilkenin, bir güvenli belirteç hizmeti (STS) tarafından verilmiş bir belirteç tarafından eklenmelidir. Media Services hello belirteçleri destekler **basit Web belirteçleri** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) biçimi ve **JSON Web belirteci** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) biçimi.

Media Services, güvenli belirteç hizmetleri sağlamaz. Özel bir STS oluşturabilir veya Microsoft Azure ACS tooissue belirteçleri yararlanın. (Bu makalede anlatıldığı gibi) hello belirteç kısıtlamasına yapılandırmasında belirtilen sorunu talepleri ve Hello STS hello belirtilen anahtara sahip bir belirteci imzalayan yapılandırılmış toocreate olmalıdır. Merhaba Media Services anahtar teslim hizmeti hello şifreleme anahtar toohello istemcisi hello belirteci geçerliyse ve hello hello belirtecinizdeki talepleri hello içerik anahtarı için yapılandırılan eşleşen döndürür.

Daha fazla bilgi için bkz.

[JWT belirteci kimlik doğrulaması](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

[Azure Media Services OWIN MVC tabanlı uygulama Azure Active Directory ile tümleştirme ve JWT talepleri temelinde içerik anahtar teslim kısıtlamak](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).

[Azure ACS tooissue belirteçlerini kullanmak](http://mingfeiy.com/acs-with-key-services).

### <a name="some-considerations-apply"></a>Bazı dikkate alınması gereken noktalar vardır:
* AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu. İçerik ve Al avantajı, dinamik paketleme ve dinamik şifreleme, akış uç noktanızı akış toostart sahip toobe hello **çalıştıran** durumu. 
* Varlığınızı Uyarlamalı bit hızlı MP4s ya da Uyarlamalı bit hızlı kesintisiz akış dosyaları içermelidir. Daha fazla bilgi için bkz: [bir varlık kodla](media-services-encode-asset.md).
* Karşıya yükleme ve kullanma, varlıkları kodlamak **AssetCreationOptions.StorageEncrypted** seçeneği.
* Toohave düşünüyorsanız gerektiren birden çok içerik anahtarı aynı hello ilkesi yapılandırması olmasından kesinlikle toocreate tek yetkilendirme ilkesi önerilen ve birden çok içerik anahtarı ile yeniden.
* Merhaba anahtar teslim hizmeti ContentKeyAuthorizationPolicy ve ilişkili nesnelerini (ilkesi seçenekleri ve kısıtlamaları) 15 dakika için önbelleğe alır.  Bir ContentKeyAuthorizationPolicy oluşturmak ve toouse "Token" kısıtlama belirtirseniz ardından test ve hello İlkesi güncelleştirmesi çok kısıtlama "Aç", hello İlkesi anahtarları toohello "Açık" Merhaba ilkesinin sürümü önce yaklaşık 15 dakika sürer.
* Varlığınızın teslim ilkesini ekler veya güncelleştirirseniz, mevcut bulucuyu (varsa) silip yeni bir bulucu oluşturmanız gerekir.
* Şu anda, aşamalı indirme şifrelenemiyor.

## <a name="aes-128-dynamic-encryption"></a>AES-128 dinamik şifreleme
### <a name="open-restriction"></a>Açık kısıtlama
Açık sınırlama hello sistem anahtar isteği yapan hello anahtar tooanyone teslim eder anlamına gelir. Bu kısıtlama sınama amacıyla yararlı olabilir.

Aşağıdaki örnek hello bir açık yetkilendirme ilkesi oluşturur ve toohello içerik anahtarı ekler.

    static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
    {
        // Create ContentKeyAuthorizationPolicy with Open restrictions
        // and create authorization policy
        IContentKeyAuthorizationPolicy policy = _context.
        ContentKeyAuthorizationPolicies.
        CreateAsync("Open Authorization Policy").Result;
        
        List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

        ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
                Name = "HLS Open Authorization Policy",
                KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                Requirements = null // no requirements needed for HLS
            };

        restrictions.Add(restriction);

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "policy", 
            ContentKeyDeliveryType.BaselineHttp, 
            restrictions, 
            "");

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);
    }


### <a name="token-restriction"></a>Belirteç kısıtlama
Bu bölümde, nasıl toocreate bir içerik anahtarı yetkilendirme ilkesini ve hello içerik anahtarı ile ilişkilendirmek açıklanmaktadır. Merhaba yetkilendirme ilkesi açıklar hello kullanıcı yetkili tooreceive hello anahtarı ise, hangi Yetkilendirme gereksinimler ölç toodetermine olması gerekir (örneğin, hello "doğrulama anahtarı" listesi hello anahtarı içermiyor hello belirtecini ile imzalandığı).

tooconfigure hello belirteç kısıtlamasına seçeneği, gereksinim duyduğunuz toouse XML toodescribe hello belirtecin yetkilendirme gereksinimleri. Merhaba belirteci kısıtlama yapılandırması XML XML Şeması aşağıdaki toohello uygun olmalıdır.

#### <a id="schema"></a>Belirteç kısıtlamasına şeması
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:complexType name="TokenClaim">
        <xs:sequence>
          <xs:element name="ClaimType" nillable="true" type="xs:string" />
          <xs:element minOccurs="0" name="ClaimValue" nillable="true" type="xs:string" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="TokenClaim" nillable="true" type="tns:TokenClaim" />
      <xs:complexType name="TokenRestrictionTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AlternateVerificationKeys" nillable="true" type="tns:ArrayOfTokenVerificationKey" />
          <xs:element name="Audience" nillable="true" type="xs:anyURI" />
          <xs:element name="Issuer" nillable="true" type="xs:anyURI" />
          <xs:element name="PrimaryVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
          <xs:element minOccurs="0" name="RequiredClaims" nillable="true" type="tns:ArrayOfTokenClaim" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="TokenRestrictionTemplate" nillable="true" type="tns:TokenRestrictionTemplate" />
      <xs:complexType name="ArrayOfTokenVerificationKey">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="TokenVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfTokenVerificationKey" nillable="true" type="tns:ArrayOfTokenVerificationKey" />
      <xs:complexType name="TokenVerificationKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="TokenVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
      <xs:complexType name="ArrayOfTokenClaim">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="TokenClaim" nillable="true" type="tns:TokenClaim" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfTokenClaim" nillable="true" type="tns:ArrayOfTokenClaim" />
      <xs:complexType name="SymmetricVerificationKey">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:TokenVerificationKey">
            <xs:sequence>
              <xs:element name="KeyValue" nillable="true" type="xs:base64Binary" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="SymmetricVerificationKey" nillable="true" type="tns:SymmetricVerificationKey" />
    </xs:schema>

Merhaba yapılandırırken **belirteci** kısıtlanmış İlkesi hello birincil doğrulama anahtarı **, belirtmeniz gerekir **veren** ve **İzleyici** parametreleri. Merhaba ** birincil doğrulama anahtarı ** içeren belirteci hello hello anahtarı ile imzalanmış **veren** hello güvenli belirteç hizmeti bu sorunları hello belirtecidir. Merhaba **İzleyici** (olarak da adlandırılan **kapsam**) hello hedefi tanımlar hello belirteç veya hello kaynak hello belirteci erişimini yetkilendirir. Merhaba Media Services anahtar teslim hizmeti bu değerleri hello belirteci hello değerleri hello şablonunda eşleştiğini doğrular. 

Kullanırken **.NET için Media Services SDK'sı**, hello kullanabilirsiniz **TokenRestrictionTemplate** sınıfı toogenerate hello kısıtlama belirteci.
Aşağıdaki örneğine hello belirteci bir kısıtlamaya sahip bir yetkilendirme ilkesi oluşturur. Bu örnekte, hello istemci içeren bir belirteç toopresent gerekir: imzalama anahtarı (VerificationKey), bir belirteç verenin ve gerekli talep.

    public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
    {
        string tokenTemplateString = GenerateTokenRequirements();

        IContentKeyAuthorizationPolicy policy = _context.
                                ContentKeyAuthorizationPolicies.
                                CreateAsync("HLS token restricted authorization policy").Result;

        List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                new List<ContentKeyAuthorizationPolicyRestriction>();

        ContentKeyAuthorizationPolicyRestriction restriction =
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Token Authorization Policy",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                    Requirements = tokenTemplateString
                };

        restrictions.Add(restriction);

        //You could have multiple options 
        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
                "Token option for HLS",
                ContentKeyDeliveryType.BaselineHttp,
                restrictions,
                null  // no key delivery data is needed for HLS
                );

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);

        return tokenTemplateString;
    }

    static private string GenerateTokenRequirements()
    {
        TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

        template.PrimaryVerificationKey = new SymmetricVerificationKey();
        template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();

        template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

        return TokenRestrictionTemplateSerializer.Serialize(template);
    }

#### <a id="test"></a>Test simgesi
Aşağıdaki Merhaba, bir test belirteci tooget hello anahtar yetkilendirme ilkesi için kullanılan belirteç kısıtlamasına hello temel.

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
    // Note, you need toopass hello key id Guid because we specified 
    // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
    Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
    Console.WriteLine();


## <a name="playready-dynamic-encryption"></a>PlayReady dinamik şifreleme
Media Services tooconfigure hello hakları ve bir kullanıcı çalışırken Merhaba PlayReady DRM çalışma zamanı tooenforce tooplay geri korumalı içeriği istediğiniz kısıtlamaları sağlar. 

İçeriğinizi PlayReady ile korurken hello özelliklerinden biri ihtiyacınız toospecify Yetkilendirme İlkesi'nde hello tanımlayan bir XML dizesi olan [PlayReady lisans şablonu](media-services-playready-license-template-overview.md). .NET için Media Services SDK'hello **PlayReadyLicenseResponseTemplate** ve **PlayReadyLicenseTemplate** sınıfları hello PlayReady lisans şablonu tanımlamanıza yardımcı olur.

[Bu konuda](media-services-protect-with-drm.md) gösterir nasıl tooencrypt, içeriğinizle **PlayReady** ve **Widevine**.

### <a name="open-restriction"></a>Açık kısıtlama
Açık sınırlama hello sistem anahtar isteği yapan hello anahtar tooanyone teslim eder anlamına gelir. Bu kısıtlama sınama amacıyla yararlı olabilir.

Aşağıdaki örnek hello bir açık yetkilendirme ilkesi oluşturur ve toohello içerik anahtarı ekler.

    static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
    {

        // Create ContentKeyAuthorizationPolicy with Open restrictions 
        // and create authorization policy          

        List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
        {
            new ContentKeyAuthorizationPolicyRestriction 
            { 
                Name = "Open", 
                KeyRestrictionType = (int)ContentKeyRestrictionType.Open, 
                Requirements = null
            }
        };

        // Configure PlayReady license template.
        string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.PlayReadyLicense,
                    restrictions, newLicenseTemplate);

        IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                    ContentKeyAuthorizationPolicies.
                    CreateAsync("Deliver Common Content Key with no restrictions").
                    Result;


        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate hello content key authorization policy with hello content key.
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;
    }

### <a name="token-restriction"></a>Belirteç kısıtlama
tooconfigure hello belirteç kısıtlamasına seçeneği, gereksinim duyduğunuz toouse XML toodescribe hello belirtecin yetkilendirme gereksinimleri. Merhaba belirteci kısıtlama yapılandırması XML toohello XML Şeması'nda gösterilen uygun olmalıdır [bu](#schema) bölümü.

    public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
    {
        string tokenTemplateString = GenerateTokenRequirements();

        IContentKeyAuthorizationPolicy policy = _context.
                                ContentKeyAuthorizationPolicies.
                                CreateAsync("HLS token restricted authorization policy").Result;

        List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
        {
            new ContentKeyAuthorizationPolicyRestriction 
            { 
                Name = "Token Authorization Policy", 
                KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                Requirements = tokenTemplateString, 
            }
        };

        // Configure PlayReady license template.
        string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.PlayReadyLicense,
                    restrictions, newLicenseTemplate);

        IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                    ContentKeyAuthorizationPolicies.
                    CreateAsync("Deliver Common Content Key with no restrictions").
                    Result;

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate hello content key authorization policy with hello content key
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;

        return tokenTemplateString;
    }

    static private string GenerateTokenRequirements()
    {

        TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

        template.PrimaryVerificationKey = new SymmetricVerificationKey();
        template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();


        template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

        return TokenRestrictionTemplateSerializer.Serialize(template);
    } 

    static private string ConfigurePlayReadyLicenseTemplate()
    {
        // hello following code configures PlayReady License Template using .NET classes
        // and returns hello XML string.

        //hello PlayReadyLicenseResponseTemplate class represents hello template for hello response sent back toohello end user. 
        //It contains a field for a custom data string between hello license server and hello application 
        //(may be useful for custom app logic) as well as a list of one or more license templates.
        PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

        // hello PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
        // toobe returned toohello end users. 
        //It contains hello data on hello content key in hello license and any rights or restrictions toobe 
        //enforced by hello PlayReady DRM runtime when using hello content key.
        PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
        //Configure whether hello license is persistent (saved in persistent storage on hello client) 
        //or non-persistent (only held in memory while hello player is using hello license).  
        licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

        // AllowTestDevices controls whether test devices can use hello license or not.  
        // If true, hello MinimumSecurityLevel property of hello license
        // is set too150.  If false (hello default), hello MinimumSecurityLevel property of hello license is set too2000.
        licenseTemplate.AllowTestDevices = true;


        // You can also configure hello Play Right in hello PlayReady license by using hello PlayReadyPlayRight class. 
        // It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions 
        // configured in hello license and on hello PlayRight itself (for playback specific policy). 
        // Much of hello policy on hello PlayRight has toodo with output restrictions 
        // which control hello types of outputs that hello content can be played over and 
        // any restrictions that must be put in place when using a given output.
        // For example, if hello DigitalVideoOnlyContentRestriction is enabled, 
        //then hello DRM runtime will only allow hello video toobe displayed over digital outputs 
        //(analog video outputs won’t be allowed toopass hello content).

        //IMPORTANT: These types of restrictions can be very powerful but can also affect hello consumer experience. 
        // If hello output protections are configured too restrictive, 
        // hello content might be unplayable on some clients. For more information, see hello PlayReady Compliance Rules document.

        // For example:
        //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

        responseTemplate.LicenseTemplates.Add(licenseTemplate);

        return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
    }


bir test belirteci hello anahtar yetkilendirme ilkesi için bkz. kullanılan hello belirteç kısıtlamasına dayalı tooget [bu](#test) bölümü. 

## <a id="types"></a>ContentKeyAuthorizationPolicy tanımlarken kullanılan türleri
### <a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType
    public enum ContentKeyDeliveryType
    {
      None = 0,
      PlayReadyLicense = 1,
      BaselineHttp = 2,
      Widevine = 3
    }

### <a id="TokenType"></a>TokenType
    public enum TokenType
    {
        Undefined = 0,
        SWT = 1,
        JWT = 2,
    }



## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a>Sonraki adım
İçerik anahtarının yetkilendirme ilkesini yapılandırmış, toohello Git [nasıl tooconfigure varlık teslim ilkesini](media-services-dotnet-configure-asset-delivery-policy.md) konu.

