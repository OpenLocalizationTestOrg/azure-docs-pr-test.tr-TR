---
title: "Media Services .NET SDK kullanarak içerik anahtarı yetkilendirme ilkesini yapılandırma | Microsoft Docs"
description: "Media Services .NET SDK kullanarak içerik anahtarının yetkilendirme ilkesini yapılandırma hakkında bilgi edinin."
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
ms.openlocfilehash: 75dd9107dca215a0b31db3d44bada69210fe9ac6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="f289c-103">Dinamik şifreleme: içerik anahtarı yetkilendirme ilkesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f289c-103">Dynamic encryption: configure content key authorization policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="f289c-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f289c-104">Overview</span></span>
<span data-ttu-id="f289c-105">Microsoft Azure Media Services, Gelişmiş Şifreleme Standardı ((128-bit şifreleme anahtarları kullanılarak) AES ile) korumalı MPEG-DASH, kesintisiz akış ve HTTP canlı akış (HLS) akışlar sunmanıza olanak sağlar veya [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="f289c-105">Microsoft Azure Media Services enables you to deliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with Advanced Encryption Standard (AES) (using 128-bit encryption keys) or [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="f289c-106">AMS Widevine DRM ile şifrelenmiş DASH akışları teslim etmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="f289c-106">AMS also enables you to deliver DASH streams encrypted with Widevine DRM.</span></span> <span data-ttu-id="f289c-107">PlayReady ve Widevine, Ortak Şifreleme (ISO/IEC 23001-7 CENC) belirtimi uyarınca şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="f289c-107">Both PlayReady and Widevine are encrypted per the Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span>

<span data-ttu-id="f289c-108">Medya Hizmetleri de sağlar bir **anahtarı/lisans teslimat hizmeti** istemcilerin AES anahtarları veya şifrelenmiş içeriği yürütmek için PlayReady/Widevine lisansları elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f289c-108">Media Services also provides a **Key/License Delivery Service** from which clients can obtain AES keys or PlayReady/Widevine licenses to play the encrypted content.</span></span>

<span data-ttu-id="f289c-109">Media Services'ın bir varlık şifrelemek istiyorsanız, bir şifreleme anahtarı ilişkilendirmeniz gerekir (**CommonEncryption** veya **EnvelopeEncryption**) varlık ile (açıklandığı gibi [burada](media-services-dotnet-create-contentkey.md)) ve anahtar için Yetkilendirme İlkeleri (Bu makalede anlatıldığı gibi) de yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f289c-109">If you want for Media Services to encrypt an asset, you need to associate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with the asset (as described [here](media-services-dotnet-create-contentkey.md)) and also configure authorization policies for the key (as described in this article).</span></span>

<span data-ttu-id="f289c-110">Bir akış player tarafından istendiğinde Media Services belirtilen anahtarı dinamik olarak içeriğinizi AES veya DRM şifreleme kullanarak şifrelemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="f289c-110">When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content using AES or DRM encryption.</span></span> <span data-ttu-id="f289c-111">Akış şifresini çözmek için player anahtar teslim hizmetinden anahtarı ister.</span><span class="sxs-lookup"><span data-stu-id="f289c-111">To decrypt the stream, the player will request the key from the key delivery service.</span></span> <span data-ttu-id="f289c-112">Kullanıcının anahtarını almak için yetkili olup olmadığına karar vermek için anahtar için belirtilen Yetkilendirme İlkeleri hizmet değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="f289c-112">To decide whether or not the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span></span>

<span data-ttu-id="f289c-113">Media Services, anahtar isteğinde bulunan kullanıcıların kimlik doğrulamasını yapmanın birden çok yöntemini destekler.</span><span class="sxs-lookup"><span data-stu-id="f289c-113">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="f289c-114">İçerik anahtarı yetkilendirme ilkesini bir veya daha fazla yetkilendirme kısıtlamaları olabilir: **açmak** veya **belirteci** kısıtlama.</span><span class="sxs-lookup"><span data-stu-id="f289c-114">The content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="f289c-115">Belirteç kısıtlamalı ilkenin beraberinde bir Güvenli Belirteç Hizmeti (STS) tarafından verilmiş bir belirteç bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f289c-115">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="f289c-116">Media Services belirteçleri destekler **basit Web belirteçleri** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) biçimi ve **JSON Web belirteci** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) biçimi.</span><span class="sxs-lookup"><span data-stu-id="f289c-116">Media Services supports tokens in the **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) format.</span></span>

<span data-ttu-id="f289c-117">Media Services, güvenli belirteç hizmetleri sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="f289c-117">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="f289c-118">Özel bir STS oluşturabilir veya Microsoft Azure ACS sorunu belirteçleri yararlanın.</span><span class="sxs-lookup"><span data-stu-id="f289c-118">You can create a custom STS or leverage Microsoft Azure ACS to issue tokens.</span></span> <span data-ttu-id="f289c-119">STS, belirteç kısıtlamasına yapılandırma dosyasında (Bu makalede anlatıldığı gibi) belirtilen belirtilen anahtarı ve sorunu talepleri imzalı bir belirteç oluşturmak için yapılandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f289c-119">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration (as described in this article).</span></span> <span data-ttu-id="f289c-120">Media Services anahtar teslim hizmeti şifreleme anahtarını istemci için belirteç geçerliyse ve içerik anahtarı için yapılandırılmış talep belirteci eşleştiğinden döndürür.</span><span class="sxs-lookup"><span data-stu-id="f289c-120">The Media Services key delivery service will return the encryption key to the client if the token is valid and the claims in the token match those configured for the content key.</span></span>

<span data-ttu-id="f289c-121">Daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="f289c-121">For more information, see</span></span>

[<span data-ttu-id="f289c-122">JWT belirteci kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="f289c-122">JWT token authentication</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="f289c-123">[Azure Media Services OWIN MVC tabanlı uygulama Azure Active Directory ile tümleştirme ve JWT talepleri temelinde içerik anahtar teslim kısıtlamak](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span><span class="sxs-lookup"><span data-stu-id="f289c-123">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="f289c-124">[Azure ACS sorunu belirteçleri kullanmak](http://mingfeiy.com/acs-with-key-services).</span><span class="sxs-lookup"><span data-stu-id="f289c-124">[Use Azure ACS to issue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="f289c-125">Bazı dikkate alınması gereken noktalar vardır:</span><span class="sxs-lookup"><span data-stu-id="f289c-125">Some considerations apply:</span></span>
* <span data-ttu-id="f289c-126">AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor hesabınızda **durduruldu** durumu.</span><span class="sxs-lookup"><span data-stu-id="f289c-126">When your AMS account is created a **default** streaming endpoint is added  to your account in the **Stopped** state.</span></span> <span data-ttu-id="f289c-127">İçeriğinizi akış başlatmak ve dinamik paketleme ve dinamik şifreleme yararlanmak için akış uç noktanızı olması sahip **çalıştıran** durumu.</span><span class="sxs-lookup"><span data-stu-id="f289c-127">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, your streaming endpoint has to be in the **Running** state.</span></span> 
* <span data-ttu-id="f289c-128">Varlığınızı Uyarlamalı bit hızlı MP4s ya da Uyarlamalı bit hızlı kesintisiz akış dosyaları içermelidir.</span><span class="sxs-lookup"><span data-stu-id="f289c-128">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="f289c-129">Daha fazla bilgi için bkz: [bir varlık kodla](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="f289c-129">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="f289c-130">Karşıya yükleme ve kullanma, varlıkları kodlamak **AssetCreationOptions.StorageEncrypted** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="f289c-130">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="f289c-131">Aynı ilke yapılandırma gerektiren birden çok içerik anahtarı oluşturmayı planlıyorsanız, tek yetkilendirme ilkesi oluşturma ve birden çok içerik anahtarı ile yeniden önemle tavsiye edilir.</span><span class="sxs-lookup"><span data-stu-id="f289c-131">If you plan to have multiple content keys that require the same policy configuration, it is strongly recommended to create a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="f289c-132">Anahtar teslim hizmeti ContentKeyAuthorizationPolicy ve ilişkili nesnelerini (ilkesi seçenekleri ve kısıtlamaları) 15 dakika için önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="f289c-132">The Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="f289c-133">Bir ContentKeyAuthorizationPolicy oluşturup, bir "Token" kısıtlama kullanılacağını belirtin, test ve ardından ilkesini "Açık" kısıtlama güncelleştirin, ilke ilkesini "Açık" sürümüne geçiş yapmadan önce yaklaşık 15 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="f289c-133">If you create a ContentKeyAuthorizationPolicy and specify to use a “Token” restriction, then test it, and then update the policy to “Open” restriction, it will take roughly 15 minutes before the policy switches to the “Open” version of the policy.</span></span>
* <span data-ttu-id="f289c-134">Varlığınızın teslim ilkesini ekler veya güncelleştirirseniz, mevcut bulucuyu (varsa) silip yeni bir bulucu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f289c-134">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="f289c-135">Şu anda, aşamalı indirme şifrelenemiyor.</span><span class="sxs-lookup"><span data-stu-id="f289c-135">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="f289c-136">AES-128 dinamik şifreleme</span><span class="sxs-lookup"><span data-stu-id="f289c-136">AES-128 Dynamic Encryption</span></span>
### <a name="open-restriction"></a><span data-ttu-id="f289c-137">Açık kısıtlama</span><span class="sxs-lookup"><span data-stu-id="f289c-137">Open Restriction</span></span>
<span data-ttu-id="f289c-138">Açık sınırlama Sistem anahtarı anahtar istekte herkes dağıtılacak anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="f289c-138">Open restriction means the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="f289c-139">Bu kısıtlama sınama amacıyla yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f289c-139">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="f289c-140">Aşağıdaki örnek, bir açık yetkilendirme ilkesi oluşturur ve içerik anahtarı ekler.</span><span class="sxs-lookup"><span data-stu-id="f289c-140">The following example creates an open authorization policy and adds it to the content key.</span></span>

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

        // Add ContentKeyAutorizationPolicy to ContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);
    }


### <a name="token-restriction"></a><span data-ttu-id="f289c-141">Belirteç kısıtlama</span><span class="sxs-lookup"><span data-stu-id="f289c-141">Token Restriction</span></span>
<span data-ttu-id="f289c-142">Bu bölümde, bir içerik anahtarı yetkilendirme ilkesi oluşturun ve içerik anahtarı ile ilişkilendirmek açıklar.</span><span class="sxs-lookup"><span data-stu-id="f289c-142">This section describes how to create a content key authorization policy and associate it with the content key.</span></span> <span data-ttu-id="f289c-143">Yetkilendirme İlkesi, kullanıcı (örneğin "doğrulama anahtarı" listede yer belirteci ile imzalandığı anahtarı yoksa) anahtarı alma yetkisi olup olmadığını belirlemek için hangi Yetkilendirme gereksinimlerin karşılanması gerekir açıklar.</span><span class="sxs-lookup"><span data-stu-id="f289c-143">The authorization policy describes what authorization requirements must be met to determine if the user is authorized to receive the key (for example, does the “verification key” list contain the key that the token was signed with).</span></span>

<span data-ttu-id="f289c-144">Belirteç kısıtlamasına seçeneği yapılandırmak için belirtecin yetkilendirme gereksinimlerini tanımlamak için bir XML kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f289c-144">To configure the token restriction option, you need to use an XML to describe the token’s authorization requirements.</span></span> <span data-ttu-id="f289c-145">Belirteç kısıtlamasına yapılandırma XML için aşağıdaki XML Şeması uygun olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f289c-145">The token restriction configuration XML must conform to the following XML schema.</span></span>

#### <span data-ttu-id="f289c-146"><a id="schema"></a>Belirteç kısıtlamasına şeması</span><span class="sxs-lookup"><span data-stu-id="f289c-146"><a id="schema"></a>Token restriction schema</span></span>
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

<span data-ttu-id="f289c-147">Yapılandırırken **belirteci** kısıtlanmış İlkesi, birincil doğrulama anahtarı **, belirtmelisiniz **veren** ve **İzleyici** parametreleri.</span><span class="sxs-lookup"><span data-stu-id="f289c-147">When configuring the **token** restricted policy, you must specify the primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="f289c-148">** Birincil doğrulama anahtarı **, belirteci imzalayan anahtarı içeren **veren** belirtecini veren güvenli belirteç hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="f289c-148">The **primary verification key **contains the key that the token was signed with, **issuer** is the secure token service that issues the token.</span></span> <span data-ttu-id="f289c-149">**İzleyici** (bazen adlı **kapsam**) belirteç veya belirteç erişim yetkisi verir kaynak amacı açıklar.</span><span class="sxs-lookup"><span data-stu-id="f289c-149">The **audience** (sometimes called **scope**) describes the intent of the token or the resource the token authorizes access to.</span></span> <span data-ttu-id="f289c-150">Media Services anahtar teslim hizmeti, bu değerleri belirteci şablon değerleri eşleştiğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="f289c-150">The Media Services key delivery service validates that these values in the token match the values in the template.</span></span> 

<span data-ttu-id="f289c-151">Kullanırken **.NET için Media Services SDK'sı**, kullanabileceğiniz **TokenRestrictionTemplate** kısıtlama belirteci üretmek için sınıf.</span><span class="sxs-lookup"><span data-stu-id="f289c-151">When using **Media Services SDK for .NET**, you can use the **TokenRestrictionTemplate** class to generate the restriction token.</span></span>
<span data-ttu-id="f289c-152">Aşağıdaki örnek, bir belirteç kısıtlamasına bir yetkilendirme ilkesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f289c-152">The following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="f289c-153">Bu örnekte, istemci içeren bir belirteç sunmak gerekecektir: imzalama anahtarı (VerificationKey), bir belirteç verenin ve gerekli talep.</span><span class="sxs-lookup"><span data-stu-id="f289c-153">In this example, the client would have to present a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

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

        // Add ContentKeyAutorizationPolicy to ContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);

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

#### <span data-ttu-id="f289c-154"><a id="test"></a>Test simgesi</span><span class="sxs-lookup"><span data-stu-id="f289c-154"><a id="test"></a>Test token</span></span>
<span data-ttu-id="f289c-155">Anahtar yetkilendirme ilkesi için kullanılan belirteç kısıtlamasına dayalı bir test belirteci almak için aşağıdakileri yapın.</span><span class="sxs-lookup"><span data-stu-id="f289c-155">To get a test token based on the token restriction that was used for the key authorization policy, do the following.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on the the data in the given TokenRestrictionTemplate.
    // Note, you need to pass the key id Guid because we specified 
    // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
    Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

    //The GenerateTestToken method returns the token without the word “Bearer” in front
    //so you have to add it in front of the token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
    Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
    Console.WriteLine();


## <a name="playready-dynamic-encryption"></a><span data-ttu-id="f289c-156">PlayReady dinamik şifreleme</span><span class="sxs-lookup"><span data-stu-id="f289c-156">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="f289c-157">Media Services hakları ve PlayReady DRM çalışma zamanı için bir kullanıcının korumalı içeriği kayıttan çalışırken uygulamak istediğinize kısıtlamaları yapılandırmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="f289c-157">Media Services enables you to configure the rights and restrictions that you want for the PlayReady DRM runtime to enforce when a user is trying to play back protected content.</span></span> 

<span data-ttu-id="f289c-158">İçeriğinizi PlayReady ile korurken, Yetkilendirme ilkesinde belirtmek için gereken şeyleri tanımlayan bir XML dizesi biri [PlayReady lisans şablonu](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f289c-158">When protecting your content with PlayReady, one of the things you need to specify in your authorization policy is an XML string that defines the [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> <span data-ttu-id="f289c-159">.NET için Media Services SDK **PlayReadyLicenseResponseTemplate** ve **PlayReadyLicenseTemplate** sınıfları, PlayReady lisans şablonu tanımlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="f289c-159">In Media Services SDK for .NET, the **PlayReadyLicenseResponseTemplate** and **PlayReadyLicenseTemplate** classes will help you define the PlayReady License Template.</span></span>

<span data-ttu-id="f289c-160">[Bu konuda](media-services-protect-with-drm.md) içeriğinizi ile şifrelemek gösterilmiştir **PlayReady** ve **Widevine**.</span><span class="sxs-lookup"><span data-stu-id="f289c-160">[This topic](media-services-protect-with-drm.md) shows how to encrypt your content with **PlayReady** and **Widevine**.</span></span>

### <a name="open-restriction"></a><span data-ttu-id="f289c-161">Açık kısıtlama</span><span class="sxs-lookup"><span data-stu-id="f289c-161">Open Restriction</span></span>
<span data-ttu-id="f289c-162">Açık sınırlama Sistem anahtarı anahtar istekte herkes dağıtılacak anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="f289c-162">Open restriction means the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="f289c-163">Bu kısıtlama sınama amacıyla yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f289c-163">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="f289c-164">Aşağıdaki örnek, bir açık yetkilendirme ilkesi oluşturur ve içerik anahtarı ekler.</span><span class="sxs-lookup"><span data-stu-id="f289c-164">The following example creates an open authorization policy and adds it to the content key.</span></span>

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

        // Associate the content key authorization policy with the content key.
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;
    }

### <a name="token-restriction"></a><span data-ttu-id="f289c-165">Belirteç kısıtlama</span><span class="sxs-lookup"><span data-stu-id="f289c-165">Token Restriction</span></span>
<span data-ttu-id="f289c-166">Belirteç kısıtlamasına seçeneği yapılandırmak için belirtecin yetkilendirme gereksinimlerini tanımlamak için bir XML kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f289c-166">To configure the token restriction option, you need to use an XML to describe the token’s authorization requirements.</span></span> <span data-ttu-id="f289c-167">XML gösterilen XML şemasına uygun olmalıdır belirteci kısıtlama Yapılandırması [bu](#schema) bölümü.</span><span class="sxs-lookup"><span data-stu-id="f289c-167">The token restriction configuration XML must conform to the XML schema shown in [this](#schema) section.</span></span>

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

        // Add ContentKeyAutorizationPolicy to ContentKey
        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate the content key authorization policy with the content key
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
        // The following code configures PlayReady License Template using .NET classes
        // and returns the XML string.

        //The PlayReadyLicenseResponseTemplate class represents the template for the response sent back to the end user. 
        //It contains a field for a custom data string between the license server and the application 
        //(may be useful for custom app logic) as well as a list of one or more license templates.
        PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

        // The PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
        // to be returned to the end users. 
        //It contains the data on the content key in the license and any rights or restrictions to be 
        //enforced by the PlayReady DRM runtime when using the content key.
        PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
        //Configure whether the license is persistent (saved in persistent storage on the client) 
        //or non-persistent (only held in memory while the player is using the license).  
        licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

        // AllowTestDevices controls whether test devices can use the license or not.  
        // If true, the MinimumSecurityLevel property of the license
        // is set to 150.  If false (the default), the MinimumSecurityLevel property of the license is set to 2000.
        licenseTemplate.AllowTestDevices = true;


        // You can also configure the Play Right in the PlayReady license by using the PlayReadyPlayRight class. 
        // It grants the user the ability to playback the content subject to the zero or more restrictions 
        // configured in the license and on the PlayRight itself (for playback specific policy). 
        // Much of the policy on the PlayRight has to do with output restrictions 
        // which control the types of outputs that the content can be played over and 
        // any restrictions that must be put in place when using a given output.
        // For example, if the DigitalVideoOnlyContentRestriction is enabled, 
        //then the DRM runtime will only allow the video to be displayed over digital outputs 
        //(analog video outputs won’t be allowed to pass the content).

        //IMPORTANT: These types of restrictions can be very powerful but can also affect the consumer experience. 
        // If the output protections are configured too restrictive, 
        // the content might be unplayable on some clients. For more information, see the PlayReady Compliance Rules document.

        // For example:
        //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

        responseTemplate.LicenseTemplates.Add(licenseTemplate);

        return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
    }


<span data-ttu-id="f289c-168">Anahtar yetkilendirme ilkesi için bkz. kullanılan belirteç kısıtlamasına dayalı bir test belirteci almak için [bu](#test) bölümü.</span><span class="sxs-lookup"><span data-stu-id="f289c-168">To get a test token based on the token restriction that was used for the key authorization policy see [this](#test) section.</span></span> 

## <span data-ttu-id="f289c-169"><a id="types"></a>ContentKeyAuthorizationPolicy tanımlarken kullanılan türleri</span><span class="sxs-lookup"><span data-stu-id="f289c-169"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="f289c-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="f289c-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="f289c-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="f289c-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
      None = 0,
      PlayReadyLicense = 1,
      BaselineHttp = 2,
      Widevine = 3
    }

### <span data-ttu-id="f289c-172"><a id="TokenType"></a>TokenType</span><span class="sxs-lookup"><span data-stu-id="f289c-172"><a id="TokenType"></a>TokenType</span></span>
    public enum TokenType
    {
        Undefined = 0,
        SWT = 1,
        JWT = 2,
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="f289c-173">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="f289c-173">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f289c-174">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="f289c-174">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="f289c-175">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="f289c-175">Next step</span></span>
<span data-ttu-id="f289c-176">İçerik anahtarının yetkilendirme ilkesini yapılandırmış, Git [varlık teslim ilkesini yapılandırmak nasıl](media-services-dotnet-configure-asset-delivery-policy.md) konu.</span><span class="sxs-lookup"><span data-stu-id="f289c-176">Now that you have configured content key's authorization policy, go to the [How to configure asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md) topic.</span></span>

