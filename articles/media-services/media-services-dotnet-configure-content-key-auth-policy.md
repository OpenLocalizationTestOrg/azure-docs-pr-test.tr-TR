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
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="c515a-103">Dinamik şifreleme: içerik anahtarı yetkilendirme ilkesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c515a-103">Dynamic encryption: configure content key authorization policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="c515a-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="c515a-104">Overview</span></span>
<span data-ttu-id="c515a-105">Microsoft Azure Media Services sağlar toodeliver MPEG-DASH, kesintisiz akış ve HTTP canlı akış (HLS) akışlar Gelişmiş Şifreleme Standardı ((128-bit şifreleme anahtarları kullanılarak) AES ile) korumalı veya [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="c515a-105">Microsoft Azure Media Services enables you toodeliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with Advanced Encryption Standard (AES) (using 128-bit encryption keys) or [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="c515a-106">AMS Ayrıca, Widevine DRM ile şifrelenmiş, toodeliver DASH akışları sağlar.</span><span class="sxs-lookup"><span data-stu-id="c515a-106">AMS also enables you toodeliver DASH streams encrypted with Widevine DRM.</span></span> <span data-ttu-id="c515a-107">PlayReady ve Widevine, ortak şifreleme (ISO/IEC 23001-7 CENC) belirtimi hello şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="c515a-107">Both PlayReady and Widevine are encrypted per hello Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span>

<span data-ttu-id="c515a-108">Medya Hizmetleri de sağlar bir **anahtarı/lisans teslimat hizmeti** hangi istemcilerin AES anahtarları elde edebilirsiniz veya PlayReady/Widevine lisansları tooplay hello şifrelenmiş içerik.</span><span class="sxs-lookup"><span data-stu-id="c515a-108">Media Services also provides a **Key/License Delivery Service** from which clients can obtain AES keys or PlayReady/Widevine licenses tooplay hello encrypted content.</span></span>

<span data-ttu-id="c515a-109">Bir varlık için Media Services tooencrypt istiyorsanız, tooassociate bir şifreleme anahtarı gerekir (**CommonEncryption** veya **EnvelopeEncryption**) hello varlık ile (açıklandığı gibi [burada](media-services-dotnet-create-contentkey.md)) ve ayrıca Yetkilendirme İlkeleri (Bu makalede anlatıldığı gibi) başlangıç anahtarı için yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c515a-109">If you want for Media Services tooencrypt an asset, you need tooassociate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with hello asset (as described [here](media-services-dotnet-create-contentkey.md)) and also configure authorization policies for hello key (as described in this article).</span></span>

<span data-ttu-id="c515a-110">Bir akış player tarafından istendiğinde Media Services belirtilen hello kullanan anahtar toodynamically AES veya DRM şifreleme kullanarak içeriğinizi şifreleyin.</span><span class="sxs-lookup"><span data-stu-id="c515a-110">When a stream is requested by a player, Media Services uses hello specified key toodynamically encrypt your content using AES or DRM encryption.</span></span> <span data-ttu-id="c515a-111">toodecrypt hello akış hello anahtar teslim hizmetinden hello anahtar hello player isteyin.</span><span class="sxs-lookup"><span data-stu-id="c515a-111">toodecrypt hello stream, hello player will request hello key from hello key delivery service.</span></span> <span data-ttu-id="c515a-112">tooget hello anahtar desteklemediğini hello kullanıcıdır toodecide yetkili, hello hizmet hello anahtar için belirtilen hello yetkilendirme ilkelerini değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="c515a-112">toodecide whether or not hello user is authorized tooget hello key, hello service evaluates hello authorization policies that you specified for hello key.</span></span>

<span data-ttu-id="c515a-113">Media Services, anahtar isteğinde bulunan kullanıcıların kimlik doğrulamasını yapmanın birden çok yöntemini destekler.</span><span class="sxs-lookup"><span data-stu-id="c515a-113">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="c515a-114">Merhaba içerik anahtarı yetkilendirme ilkesini bir veya daha fazla yetkilendirme kısıtlamaları olabilir: **açmak** veya **belirteci** kısıtlama.</span><span class="sxs-lookup"><span data-stu-id="c515a-114">hello content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="c515a-115">Merhaba belirteç kısıtlamalı ilkenin, bir güvenli belirteç hizmeti (STS) tarafından verilmiş bir belirteç tarafından eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="c515a-115">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="c515a-116">Media Services hello belirteçleri destekler **basit Web belirteçleri** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) biçimi ve **JSON Web belirteci** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) biçimi.</span><span class="sxs-lookup"><span data-stu-id="c515a-116">Media Services supports tokens in hello **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) format.</span></span>

<span data-ttu-id="c515a-117">Media Services, güvenli belirteç hizmetleri sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="c515a-117">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="c515a-118">Özel bir STS oluşturabilir veya Microsoft Azure ACS tooissue belirteçleri yararlanın.</span><span class="sxs-lookup"><span data-stu-id="c515a-118">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="c515a-119">(Bu makalede anlatıldığı gibi) hello belirteç kısıtlamasına yapılandırmasında belirtilen sorunu talepleri ve Hello STS hello belirtilen anahtara sahip bir belirteci imzalayan yapılandırılmış toocreate olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c515a-119">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration (as described in this article).</span></span> <span data-ttu-id="c515a-120">Merhaba Media Services anahtar teslim hizmeti hello şifreleme anahtar toohello istemcisi hello belirteci geçerliyse ve hello hello belirtecinizdeki talepleri hello içerik anahtarı için yapılandırılan eşleşen döndürür.</span><span class="sxs-lookup"><span data-stu-id="c515a-120">hello Media Services key delivery service will return hello encryption key toohello client if hello token is valid and hello claims in hello token match those configured for hello content key.</span></span>

<span data-ttu-id="c515a-121">Daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="c515a-121">For more information, see</span></span>

[<span data-ttu-id="c515a-122">JWT belirteci kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="c515a-122">JWT token authentication</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="c515a-123">[Azure Media Services OWIN MVC tabanlı uygulama Azure Active Directory ile tümleştirme ve JWT talepleri temelinde içerik anahtar teslim kısıtlamak](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span><span class="sxs-lookup"><span data-stu-id="c515a-123">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="c515a-124">[Azure ACS tooissue belirteçlerini kullanmak](http://mingfeiy.com/acs-with-key-services).</span><span class="sxs-lookup"><span data-stu-id="c515a-124">[Use Azure ACS tooissue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="c515a-125">Bazı dikkate alınması gereken noktalar vardır:</span><span class="sxs-lookup"><span data-stu-id="c515a-125">Some considerations apply:</span></span>
* <span data-ttu-id="c515a-126">AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu.</span><span class="sxs-lookup"><span data-stu-id="c515a-126">When your AMS account is created a **default** streaming endpoint is added  tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="c515a-127">İçerik ve Al avantajı, dinamik paketleme ve dinamik şifreleme, akış uç noktanızı akış toostart sahip toobe hello **çalıştıran** durumu.</span><span class="sxs-lookup"><span data-stu-id="c515a-127">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, your streaming endpoint has toobe in hello **Running** state.</span></span> 
* <span data-ttu-id="c515a-128">Varlığınızı Uyarlamalı bit hızlı MP4s ya da Uyarlamalı bit hızlı kesintisiz akış dosyaları içermelidir.</span><span class="sxs-lookup"><span data-stu-id="c515a-128">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="c515a-129">Daha fazla bilgi için bkz: [bir varlık kodla](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="c515a-129">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="c515a-130">Karşıya yükleme ve kullanma, varlıkları kodlamak **AssetCreationOptions.StorageEncrypted** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="c515a-130">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="c515a-131">Toohave düşünüyorsanız gerektiren birden çok içerik anahtarı aynı hello ilkesi yapılandırması olmasından kesinlikle toocreate tek yetkilendirme ilkesi önerilen ve birden çok içerik anahtarı ile yeniden.</span><span class="sxs-lookup"><span data-stu-id="c515a-131">If you plan toohave multiple content keys that require hello same policy configuration, it is strongly recommended toocreate a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="c515a-132">Merhaba anahtar teslim hizmeti ContentKeyAuthorizationPolicy ve ilişkili nesnelerini (ilkesi seçenekleri ve kısıtlamaları) 15 dakika için önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="c515a-132">hello Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="c515a-133">Bir ContentKeyAuthorizationPolicy oluşturmak ve toouse "Token" kısıtlama belirtirseniz ardından test ve hello İlkesi güncelleştirmesi çok kısıtlama "Aç", hello İlkesi anahtarları toohello "Açık" Merhaba ilkesinin sürümü önce yaklaşık 15 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="c515a-133">If you create a ContentKeyAuthorizationPolicy and specify toouse a “Token” restriction, then test it, and then update hello policy too“Open” restriction, it will take roughly 15 minutes before hello policy switches toohello “Open” version of hello policy.</span></span>
* <span data-ttu-id="c515a-134">Varlığınızın teslim ilkesini ekler veya güncelleştirirseniz, mevcut bulucuyu (varsa) silip yeni bir bulucu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c515a-134">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="c515a-135">Şu anda, aşamalı indirme şifrelenemiyor.</span><span class="sxs-lookup"><span data-stu-id="c515a-135">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="c515a-136">AES-128 dinamik şifreleme</span><span class="sxs-lookup"><span data-stu-id="c515a-136">AES-128 Dynamic Encryption</span></span>
### <a name="open-restriction"></a><span data-ttu-id="c515a-137">Açık kısıtlama</span><span class="sxs-lookup"><span data-stu-id="c515a-137">Open Restriction</span></span>
<span data-ttu-id="c515a-138">Açık sınırlama hello sistem anahtar isteği yapan hello anahtar tooanyone teslim eder anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="c515a-138">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="c515a-139">Bu kısıtlama sınama amacıyla yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="c515a-139">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="c515a-140">Aşağıdaki örnek hello bir açık yetkilendirme ilkesi oluşturur ve toohello içerik anahtarı ekler.</span><span class="sxs-lookup"><span data-stu-id="c515a-140">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

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


### <a name="token-restriction"></a><span data-ttu-id="c515a-141">Belirteç kısıtlama</span><span class="sxs-lookup"><span data-stu-id="c515a-141">Token Restriction</span></span>
<span data-ttu-id="c515a-142">Bu bölümde, nasıl toocreate bir içerik anahtarı yetkilendirme ilkesini ve hello içerik anahtarı ile ilişkilendirmek açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c515a-142">This section describes how toocreate a content key authorization policy and associate it with hello content key.</span></span> <span data-ttu-id="c515a-143">Merhaba yetkilendirme ilkesi açıklar hello kullanıcı yetkili tooreceive hello anahtarı ise, hangi Yetkilendirme gereksinimler ölç toodetermine olması gerekir (örneğin, hello "doğrulama anahtarı" listesi hello anahtarı içermiyor hello belirtecini ile imzalandığı).</span><span class="sxs-lookup"><span data-stu-id="c515a-143">hello authorization policy describes what authorization requirements must be met toodetermine if hello user is authorized tooreceive hello key (for example, does hello “verification key” list contain hello key that hello token was signed with).</span></span>

<span data-ttu-id="c515a-144">tooconfigure hello belirteç kısıtlamasına seçeneği, gereksinim duyduğunuz toouse XML toodescribe hello belirtecin yetkilendirme gereksinimleri.</span><span class="sxs-lookup"><span data-stu-id="c515a-144">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="c515a-145">Merhaba belirteci kısıtlama yapılandırması XML XML Şeması aşağıdaki toohello uygun olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c515a-145">hello token restriction configuration XML must conform toohello following XML schema.</span></span>

#### <span data-ttu-id="c515a-146"><a id="schema"></a>Belirteç kısıtlamasına şeması</span><span class="sxs-lookup"><span data-stu-id="c515a-146"><a id="schema"></a>Token restriction schema</span></span>
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

<span data-ttu-id="c515a-147">Merhaba yapılandırırken **belirteci** kısıtlanmış İlkesi hello birincil doğrulama anahtarı **, belirtmeniz gerekir **veren** ve **İzleyici** parametreleri.</span><span class="sxs-lookup"><span data-stu-id="c515a-147">When configuring hello **token** restricted policy, you must specify hello primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="c515a-148">Merhaba ** birincil doğrulama anahtarı ** içeren belirteci hello hello anahtarı ile imzalanmış **veren** hello güvenli belirteç hizmeti bu sorunları hello belirtecidir.</span><span class="sxs-lookup"><span data-stu-id="c515a-148">hello **primary verification key **contains hello key that hello token was signed with, **issuer** is hello secure token service that issues hello token.</span></span> <span data-ttu-id="c515a-149">Merhaba **İzleyici** (olarak da adlandırılan **kapsam**) hello hedefi tanımlar hello belirteç veya hello kaynak hello belirteci erişimini yetkilendirir.</span><span class="sxs-lookup"><span data-stu-id="c515a-149">hello **audience** (sometimes called **scope**) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="c515a-150">Merhaba Media Services anahtar teslim hizmeti bu değerleri hello belirteci hello değerleri hello şablonunda eşleştiğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="c515a-150">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span> 

<span data-ttu-id="c515a-151">Kullanırken **.NET için Media Services SDK'sı**, hello kullanabilirsiniz **TokenRestrictionTemplate** sınıfı toogenerate hello kısıtlama belirteci.</span><span class="sxs-lookup"><span data-stu-id="c515a-151">When using **Media Services SDK for .NET**, you can use hello **TokenRestrictionTemplate** class toogenerate hello restriction token.</span></span>
<span data-ttu-id="c515a-152">Aşağıdaki örneğine hello belirteci bir kısıtlamaya sahip bir yetkilendirme ilkesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c515a-152">hello following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="c515a-153">Bu örnekte, hello istemci içeren bir belirteç toopresent gerekir: imzalama anahtarı (VerificationKey), bir belirteç verenin ve gerekli talep.</span><span class="sxs-lookup"><span data-stu-id="c515a-153">In this example, hello client would have toopresent a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

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

#### <span data-ttu-id="c515a-154"><a id="test"></a>Test simgesi</span><span class="sxs-lookup"><span data-stu-id="c515a-154"><a id="test"></a>Test token</span></span>
<span data-ttu-id="c515a-155">Aşağıdaki Merhaba, bir test belirteci tooget hello anahtar yetkilendirme ilkesi için kullanılan belirteç kısıtlamasına hello temel.</span><span class="sxs-lookup"><span data-stu-id="c515a-155">tooget a test token based on hello token restriction that was used for hello key authorization policy, do hello following.</span></span>

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


## <a name="playready-dynamic-encryption"></a><span data-ttu-id="c515a-156">PlayReady dinamik şifreleme</span><span class="sxs-lookup"><span data-stu-id="c515a-156">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="c515a-157">Media Services tooconfigure hello hakları ve bir kullanıcı çalışırken Merhaba PlayReady DRM çalışma zamanı tooenforce tooplay geri korumalı içeriği istediğiniz kısıtlamaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="c515a-157">Media Services enables you tooconfigure hello rights and restrictions that you want for hello PlayReady DRM runtime tooenforce when a user is trying tooplay back protected content.</span></span> 

<span data-ttu-id="c515a-158">İçeriğinizi PlayReady ile korurken hello özelliklerinden biri ihtiyacınız toospecify Yetkilendirme İlkesi'nde hello tanımlayan bir XML dizesi olan [PlayReady lisans şablonu](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c515a-158">When protecting your content with PlayReady, one of hello things you need toospecify in your authorization policy is an XML string that defines hello [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> <span data-ttu-id="c515a-159">.NET için Media Services SDK'hello **PlayReadyLicenseResponseTemplate** ve **PlayReadyLicenseTemplate** sınıfları hello PlayReady lisans şablonu tanımlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="c515a-159">In Media Services SDK for .NET, hello **PlayReadyLicenseResponseTemplate** and **PlayReadyLicenseTemplate** classes will help you define hello PlayReady License Template.</span></span>

<span data-ttu-id="c515a-160">[Bu konuda](media-services-protect-with-drm.md) gösterir nasıl tooencrypt, içeriğinizle **PlayReady** ve **Widevine**.</span><span class="sxs-lookup"><span data-stu-id="c515a-160">[This topic](media-services-protect-with-drm.md) shows how tooencrypt your content with **PlayReady** and **Widevine**.</span></span>

### <a name="open-restriction"></a><span data-ttu-id="c515a-161">Açık kısıtlama</span><span class="sxs-lookup"><span data-stu-id="c515a-161">Open Restriction</span></span>
<span data-ttu-id="c515a-162">Açık sınırlama hello sistem anahtar isteği yapan hello anahtar tooanyone teslim eder anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="c515a-162">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="c515a-163">Bu kısıtlama sınama amacıyla yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="c515a-163">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="c515a-164">Aşağıdaki örnek hello bir açık yetkilendirme ilkesi oluşturur ve toohello içerik anahtarı ekler.</span><span class="sxs-lookup"><span data-stu-id="c515a-164">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

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

### <a name="token-restriction"></a><span data-ttu-id="c515a-165">Belirteç kısıtlama</span><span class="sxs-lookup"><span data-stu-id="c515a-165">Token Restriction</span></span>
<span data-ttu-id="c515a-166">tooconfigure hello belirteç kısıtlamasına seçeneği, gereksinim duyduğunuz toouse XML toodescribe hello belirtecin yetkilendirme gereksinimleri.</span><span class="sxs-lookup"><span data-stu-id="c515a-166">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="c515a-167">Merhaba belirteci kısıtlama yapılandırması XML toohello XML Şeması'nda gösterilen uygun olmalıdır [bu](#schema) bölümü.</span><span class="sxs-lookup"><span data-stu-id="c515a-167">hello token restriction configuration XML must conform toohello XML schema shown in [this](#schema) section.</span></span>

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


<span data-ttu-id="c515a-168">bir test belirteci hello anahtar yetkilendirme ilkesi için bkz. kullanılan hello belirteç kısıtlamasına dayalı tooget [bu](#test) bölümü.</span><span class="sxs-lookup"><span data-stu-id="c515a-168">tooget a test token based on hello token restriction that was used for hello key authorization policy see [this](#test) section.</span></span> 

## <span data-ttu-id="c515a-169"><a id="types"></a>ContentKeyAuthorizationPolicy tanımlarken kullanılan türleri</span><span class="sxs-lookup"><span data-stu-id="c515a-169"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="c515a-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="c515a-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="c515a-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="c515a-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
      None = 0,
      PlayReadyLicense = 1,
      BaselineHttp = 2,
      Widevine = 3
    }

### <span data-ttu-id="c515a-172"><a id="TokenType"></a>TokenType</span><span class="sxs-lookup"><span data-stu-id="c515a-172"><a id="TokenType"></a>TokenType</span></span>
    public enum TokenType
    {
        Undefined = 0,
        SWT = 1,
        JWT = 2,
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="c515a-173">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="c515a-173">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c515a-174">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="c515a-174">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="c515a-175">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="c515a-175">Next step</span></span>
<span data-ttu-id="c515a-176">İçerik anahtarının yetkilendirme ilkesini yapılandırmış, toohello Git [nasıl tooconfigure varlık teslim ilkesini](media-services-dotnet-configure-asset-delivery-policy.md) konu.</span><span class="sxs-lookup"><span data-stu-id="c515a-176">Now that you have configured content key's authorization policy, go toohello [How tooconfigure asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md) topic.</span></span>

