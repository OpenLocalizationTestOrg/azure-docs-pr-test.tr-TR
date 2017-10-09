---
title: "aaaUse Azure Media Services toodeliver DRM lisansları veya AES anahtarları"
description: "Bu makalede Azure Media Services (AMS) toodeliver PlayReady ve/veya Widevine lisansları ve AES anahtarları kullanabilirsiniz ancak (kodlama, şifreleme, akış) rest hello nasıl şirket içi sunucularınızı kullanma."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 8546c2c1-430b-4254-a88d-4436a83f9192
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: a81da2973c79e5182ae58aeca7a0f14f3fc7c9ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-services-toodeliver-drm-licenses-or-aes-keys"></a><span data-ttu-id="e1617-103">Azure Media Services toodeliver DRM lisansları veya AES anahtarları kullanın</span><span class="sxs-lookup"><span data-stu-id="e1617-103">Use Azure Media Services toodeliver DRM licenses or AES keys</span></span>
<span data-ttu-id="e1617-104">Azure Media Services (AMS) tooingest sağlar, kodlama, içerik koruma ekleyin ve içeriğinizin akışını (bkz [bu](media-services-protect-with-drm.md) makale Ayrıntılar için).</span><span class="sxs-lookup"><span data-stu-id="e1617-104">Azure Media Services (AMS) enables you tooingest, encode, add content protection, and stream your content (see [this](media-services-protect-with-drm.md) article for details).</span></span> <span data-ttu-id="e1617-105">Ancak, yalnızca toouse AMS toodeliver lisansları ve/veya anahtarları istediğiniz ve kodlama, şifreleme ve kendi şirket içi sunucular kullanarak akış müşteriler vardır.</span><span class="sxs-lookup"><span data-stu-id="e1617-105">However, there are customers who only want toouse AMS toodeliver licenses and/or keys and do encoding, encrypting and streaming using their on-premises servers.</span></span> <span data-ttu-id="e1617-106">Bu makalede nasıl AMS toodeliver PlayReady ve/veya Widevine lisansları kullanabilirsiniz ancak geri kalan şirket içi sunucularınızla hello açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e1617-106">This article describes how you can use AMS toodeliver PlayReady and/or Widevine licenses but do hello rest with your on-premises servers.</span></span> 

## <a name="overview"></a><span data-ttu-id="e1617-107">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="e1617-107">Overview</span></span>
<span data-ttu-id="e1617-108">Media Services, PlayReady ve Widevine DRM lisansları ve AES-128 anahtarları teslim etmek için bir hizmet sunar.</span><span class="sxs-lookup"><span data-stu-id="e1617-108">Media Services provides a service for delivering PlayReady and Widevine DRM licenses and AES-128 keys.</span></span> <span data-ttu-id="e1617-109">Media Services de hello haklarını yapılandırmanıza olanak tanıyan API'ler sağlar ve hello DRM korumalı içeriği hello DRM çalışma zamanı tooenforce için bir kullanıcı istediğiniz kısıtlamaları geri kazanır.</span><span class="sxs-lookup"><span data-stu-id="e1617-109">Media Services also provides APIs that let you configure hello rights and restrictions that you want for hello DRM runtime tooenforce when a user plays back hello DRM protected content.</span></span> <span data-ttu-id="e1617-110">Bir kullanıcı istekleri hello korunan içerik, Merhaba oynatıcı uygulaması hello AMS lisans hizmetinden bir lisans ister.</span><span class="sxs-lookup"><span data-stu-id="e1617-110">When a user requests hello protected content, hello player application will request a license from hello AMS license service.</span></span> <span data-ttu-id="e1617-111">(yetkiliyse) hello AMS lisans hizmeti hello lisans toohello player gönderirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1617-111">hello AMS license service will issue hello license toohello player (if it is authorized).</span></span> <span data-ttu-id="e1617-112">Merhaba PlayReady ve Widevine lisansları hello istemci player toodecrypt ve akış Merhaba içeriğine tarafından kullanılan hello şifre çözme anahtarını içerir.</span><span class="sxs-lookup"><span data-stu-id="e1617-112">hello PlayReady and Widevine licenses contain hello decryption key that can be used by hello client player toodecrypt and stream hello content.</span></span>

<span data-ttu-id="e1617-113">Media Services lisans ya da anahtar istekleri yapabilen Kullanıcıları yetkilendirmek, birden çok yöntemini destekler.</span><span class="sxs-lookup"><span data-stu-id="e1617-113">Media Services supports multiple ways of authorizing users who make license or key requests.</span></span> <span data-ttu-id="e1617-114">Merhaba içerik anahtarının yetkilendirme ilkesini yapılandırın ve hello İlkesi, bir veya daha fazla kısıtlamaları sahip olabilir: açık veya belirteç kısıtlama.</span><span class="sxs-lookup"><span data-stu-id="e1617-114">You configure hello content key's authorization policy and hello policy could have one or more restrictions: open or token restriction.</span></span> <span data-ttu-id="e1617-115">Merhaba belirteç kısıtlamalı ilkenin, bir güvenli belirteç hizmeti (STS) tarafından verilmiş bir belirteç tarafından eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="e1617-115">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="e1617-116">Media Services, hello basit Web belirteçleri (SWT) biçimi ve JSON Web Token (JWT) biçimlerindeki belirteçleri destekler.</span><span class="sxs-lookup"><span data-stu-id="e1617-116">Media Services supports tokens in hello Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span>

<span data-ttu-id="e1617-117">Merhaba Aşağıdaki diyagramda hello ana adımlar tootake toouse AMS toodeliver PlayReady ve/veya Widevine lisansları gerekir, ancak geri kalan şirket içi sunucularınızla hello gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e1617-117">hello following diagram shows hello main steps you need tootake toouse AMS toodeliver PlayReady and/or Widevine licenses but do hello rest with your on-premises servers.</span></span>

![PlayReady ile koruma](./media/media-services-deliver-keys-and-licenses/media-services-diagram1.png)

## <a name="download-sample"></a><span data-ttu-id="e1617-119">Örnek indirme</span><span class="sxs-lookup"><span data-stu-id="e1617-119">Download sample</span></span>
<span data-ttu-id="e1617-120">Bu makalede açıklanan hello örnek indirebilirsiniz [burada](https://github.com/Azure/media-services-dotnet-deliver-drm-licenses).</span><span class="sxs-lookup"><span data-stu-id="e1617-120">You can download hello sample described in this article from [here](https://github.com/Azure/media-services-dotnet-deliver-drm-licenses).</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="e1617-121">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e1617-121">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="e1617-122">Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="e1617-122">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="e1617-123">Öğeleri çok aşağıdaki hello eklemek**appSettings** app.config dosyasında tanımlanan:</span><span class="sxs-lookup"><span data-stu-id="e1617-123">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

    <span data-ttu-id="e1617-124"><add key="Issuer" value="http://testacs.com"/> <add key="Audience" value="urn:test"/></span><span class="sxs-lookup"><span data-stu-id="e1617-124"><add key="Issuer" value="http://testacs.com"/> <add key="Audience" value="urn:test"/></span></span>

## <a name="net-code-example"></a><span data-ttu-id="e1617-125">.NET kodu örneği</span><span class="sxs-lookup"><span data-stu-id="e1617-125">.NET code example</span></span>

<span data-ttu-id="e1617-126">Aşağıdaki kod örneğine hello nasıl toocreate bir ortak anahtar içerik ve PlayReady veya Widevine lisans edinme URL'si almak gösterir.</span><span class="sxs-lookup"><span data-stu-id="e1617-126">hello following code example shows how toocreate a common content key and get PlayReady or Widevine license acquisition URLs.</span></span> <span data-ttu-id="e1617-127">Tooget ihtiyacınız hello AMS bilgilerinden parçalarını aşağıdaki ve şirket içi sunucunuzu yapılandırın: **içerik anahtarı**, **anahtarı kimliği**, **lisans edinme URL'si**.</span><span class="sxs-lookup"><span data-stu-id="e1617-127">You need tooget hello following pieces of information from AMS and configure your on-premises server: **content key**, **key id**, **license acquisition URL**.</span></span> <span data-ttu-id="e1617-128">Şirket içi sunucunuzu yapılandırdıktan sonra kendi akış sunucusundan akış.</span><span class="sxs-lookup"><span data-stu-id="e1617-128">Once you configure your on-premises server, you could stream from your own streaming server.</span></span> <span data-ttu-id="e1617-129">Merhaba şifrelenmiş akış noktaları tooAMS lisans sunucusu bu yana, player AMS lisans ister.</span><span class="sxs-lookup"><span data-stu-id="e1617-129">Since hello encrypted stream points tooAMS license server, your player will request a license from AMS.</span></span> <span data-ttu-id="e1617-130">Belirteç kimlik doğrulamasını seçerseniz, hello AMS lisans sunucusu HTTPS gönderilen hello belirteci doğrular ve (geçerli ise) hello lisans geri tooyour player teslim eder.</span><span class="sxs-lookup"><span data-stu-id="e1617-130">If you choose token authentication, hello AMS license server will validate hello token you sent through HTTPS and (if valid) will deliver hello license back tooyour player.</span></span> <span data-ttu-id="e1617-131">(Merhaba kod örneği yalnızca nasıl toocreate bir ortak anahtar içerik ve PlayReady veya Widevine lisans edinme URL'si almak gösterir.</span><span class="sxs-lookup"><span data-stu-id="e1617-131">(hello code example only shows how toocreate a common content key and  get PlayReady or Widevine license acquisition URLs.</span></span> <span data-ttu-id="e1617-132">Toodelivery AES-128 anahtarları istiyorsanız, toocreate Zarf içerik anahtarı gerekir ve bir anahtar alım URL'sini alma ve [bu](media-services-protect-with-aes128.md) makalesi gösterir nasıl toodo da).</span><span class="sxs-lookup"><span data-stu-id="e1617-132">If you want toodelivery AES-128 keys, you need toocreate an envelope content key and get a key acquisition URL and [this](media-services-protect-with-aes128.md) article shows how toodo it).</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.Widevine;
    using Newtonsoft.Json;

    namespace DeliverDRMLicenses
    {
        class Program
        {
            // Read values from hello App.config file.
            private static readonly string _AADTenantDomain =
                ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
                ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            private static readonly Uri _sampleIssuer =
                new Uri(ConfigurationManager.AppSettings["Issuer"]);
            private static readonly Uri _sampleAudience =
                new Uri(ConfigurationManager.AppSettings["Audience"]);

            // Field for service context.
            private static CloudMediaContext _context = null;

            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                bool tokenRestriction = true;
                string tokenTemplateString = null;


                IContentKey key = CreateCommonTypeContentKey();

                // Print out hello key ID and Key in base64 string format
                Console.WriteLine("Created key {0} with key value {1} ",
                    key.Id, System.Convert.ToBase64String(key.GetClearKeyValue()));

                Console.WriteLine("PlayReady License Key delivery URL: {0}",
                    key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense));

                Console.WriteLine("Widevine License Key delivery URL: {0}",
                    key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine));

                if (tokenRestriction)
                    tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
                else
                    AddOpenAuthorizationPolicy(key);

                Console.WriteLine("Added authorization policy: {0}",
                    key.AuthorizationPolicyId);
                Console.WriteLine();
                Console.ReadLine();
            }

            static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
            {

                // Create ContentKeyAuthorizationPolicy with Open restrictions 
                // and create authorization policy          

                List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                    new List<ContentKeyAuthorizationPolicyRestriction>
                {
                        new ContentKeyAuthorizationPolicyRestriction
                        {
                            Name = "Open",
                            KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                            Requirements = null
                        }
                };

                // Configure PlayReady and Widevine license templates.
                string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

                string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

                IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("",
                        ContentKeyDeliveryType.PlayReadyLicense,
                            restrictions, PlayReadyLicenseTemplate);

                IContentKeyAuthorizationPolicyOption WidevinePolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("",
                        ContentKeyDeliveryType.Widevine,
                        restrictions, WidevineLicenseTemplate);

                IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                            ContentKeyAuthorizationPolicies.
                            CreateAsync("Deliver Common Content Key with no restrictions").
                            Result;


                contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
                contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);
                // Associate hello content key authorization policy with hello content key.
                contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
                contentKey = contentKey.UpdateAsync().Result;
            }

            public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
            {
                string tokenTemplateString = GenerateTokenRequirements();

                List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                    new List<ContentKeyAuthorizationPolicyRestriction>
                {
                        new ContentKeyAuthorizationPolicyRestriction
                        {
                            Name = "Token Authorization Policy",
                            KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                            Requirements = tokenTemplateString,
                        }
                };

                // Configure PlayReady and Widevine license templates.
                string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

                string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

                IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                        ContentKeyDeliveryType.PlayReadyLicense,
                            restrictions, PlayReadyLicenseTemplate);

                IContentKeyAuthorizationPolicyOption WidevinePolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                        ContentKeyDeliveryType.Widevine,
                            restrictions, WidevineLicenseTemplate);

                IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                            ContentKeyAuthorizationPolicies.
                            CreateAsync("Deliver Common Content Key with token restrictions").
                            Result;

                contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
                contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);

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

                //hello PlayReadyLicenseResponseTemplate class represents hello template 
                //for hello response sent back toohello end user. 
                //It contains a field for a custom data string between hello license server 
                //and hello application (may be useful for custom app logic) 
                //as well as a list of one or more license templates.

                PlayReadyLicenseResponseTemplate responseTemplate =
                    new PlayReadyLicenseResponseTemplate();

                // hello PlayReadyLicenseTemplate class represents a license template 
                // for creating PlayReady licenses
                // toobe returned toohello end users. 
                // It contains hello data on hello content key in hello license 
                // and any rights or restrictions toobe 
                // enforced by hello PlayReady DRM runtime when using hello content key.
                PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();

                // Configure whether hello license is persistent 
                // (saved in persistent storage on hello client) 
                // or non-persistent (only held in memory while hello player is using hello license).  
                licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

                // AllowTestDevices controls whether test devices can use hello license or not.  
                // If true, hello MinimumSecurityLevel property of hello license
                // is set too150.  If false (hello default), 
                // hello MinimumSecurityLevel property of hello license is set too2000.
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

                // IMPORTANT: These types of restrictions can be very powerful 
                // but can also affect hello consumer experience. 
                // If hello output protections are configured too restrictive, 
                // hello content might be unplayable on some clients. 
                // For more information, see hello PlayReady Compliance Rules document.

                // For example:
                //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

                responseTemplate.LicenseTemplates.Add(licenseTemplate);

                return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
            }


            private static string ConfigureWidevineLicenseTemplate()
            {
                var template = new WidevineMessage
                {
                    allowed_track_types = AllowedTrackTypes.SD_HD,
                    content_key_specs = new[]
                    {
                            new ContentKeySpecs
                            {
                                required_output_protection =
                                    new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                                security_level = 1,
                                track_type = "SD"
                            }
                        },
                    policy_overrides = new
                    {
                        can_play = true,
                        can_persist = true,
                        can_renew = false
                    }
                };

                string configuration = JsonConvert.SerializeObject(template);
                return configuration;
            }


            static public IContentKey CreateCommonTypeContentKey()
            {
                // Create envelope encryption content key
                Guid keyId = Guid.NewGuid();
                byte[] contentKey = GetRandomBuffer(16);

                IContentKey key = _context.ContentKeys.Create(
                                        keyId,
                                        contentKey,
                                        "ContentKey",
                                        ContentKeyType.CommonEncryption);

                return key;
            }

            static private byte[] GetRandomBuffer(int length)
            {
                var returnValue = new byte[length];

                using (var rng =
                    new System.Security.Cryptography.RNGCryptoServiceProvider())
                {
                    rng.GetBytes(returnValue);
                }

                return returnValue;
            }
        }
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="e1617-133">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="e1617-133">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e1617-134">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="e1617-134">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="e1617-135">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="e1617-135">See also</span></span>
[<span data-ttu-id="e1617-136">PlayReady ve/veya Widevine dinamik ortak şifreleme kullanma</span><span class="sxs-lookup"><span data-stu-id="e1617-136">Using PlayReady and/or Widevine Dynamic Common Encryption</span></span>](media-services-protect-with-drm.md)

[<span data-ttu-id="e1617-137">AES-128 dinamik şifreleme ve anahtar teslim hizmeti kullanma</span><span class="sxs-lookup"><span data-stu-id="e1617-137">Using AES-128 Dynamic Encryption and Key Delivery Service</span></span>](media-services-protect-with-aes128.md)

[<span data-ttu-id="e1617-138">İş ortakları toodeliver Widevine lisansları tooAzure Media Services'i kullanma</span><span class="sxs-lookup"><span data-stu-id="e1617-138">Using partners toodeliver Widevine licenses tooAzure Media Services</span></span>](media-services-licenses-partner-integration.md)

