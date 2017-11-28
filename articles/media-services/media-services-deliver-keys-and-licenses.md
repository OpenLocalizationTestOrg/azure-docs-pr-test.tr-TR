---
title: "DRM lisansları veya AES anahtarları göndermek için Azure Media Services'i kullanma"
description: "Bu makalede PlayReady sağlamak üzere Azure Media Services (AMS) nasıl kullanabileceğinizi açıklar ve/veya Widevine lisansları ve AES anahtarları (kodlama, şifreleme, akış) rest yapmak ancak şirket içi sunucularınızı kullanma."
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
ms.openlocfilehash: 263a381dc72105eea60ad9b39434599ff04a4531
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-media-services-to-deliver-drm-licenses-or-aes-keys"></a><span data-ttu-id="f321f-103">DRM lisansları veya AES anahtarları göndermek için Azure Media Services'i kullanma</span><span class="sxs-lookup"><span data-stu-id="f321f-103">Use Azure Media Services to deliver DRM licenses or AES keys</span></span>
<span data-ttu-id="f321f-104">Azure Media Services (AMS), alma, kodlama, içerik koruma ekleyin ve içeriğinizin akışını sağlar (bkz [bu](media-services-protect-with-drm.md) makale Ayrıntılar için).</span><span class="sxs-lookup"><span data-stu-id="f321f-104">Azure Media Services (AMS) enables you to ingest, encode, add content protection, and stream your content (see [this](media-services-protect-with-drm.md) article for details).</span></span> <span data-ttu-id="f321f-105">Ancak, yalnızca AMS lisans ve/veya anahtarları teslim etmek ve kodlama, şifreleme ve kendi şirket içi sunucular kullanarak akış yapmak için kullanmak isteyen müşteriler vardır.</span><span class="sxs-lookup"><span data-stu-id="f321f-105">However, there are customers who only want to use AMS to deliver licenses and/or keys and do encoding, encrypting and streaming using their on-premises servers.</span></span> <span data-ttu-id="f321f-106">Bu makalede, PlayReady ve/veya Widevine lisansları teslim ancak geri kalan şirket içi sunucularınızla yapmak için AMS nasıl kullanabileceğiniz açıklanır.</span><span class="sxs-lookup"><span data-stu-id="f321f-106">This article describes how you can use AMS to deliver PlayReady and/or Widevine licenses but do the rest with your on-premises servers.</span></span> 

## <a name="overview"></a><span data-ttu-id="f321f-107">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f321f-107">Overview</span></span>
<span data-ttu-id="f321f-108">Media Services, PlayReady ve Widevine DRM lisansları ve AES-128 anahtarları teslim etmek için bir hizmet sunar.</span><span class="sxs-lookup"><span data-stu-id="f321f-108">Media Services provides a service for delivering PlayReady and Widevine DRM licenses and AES-128 keys.</span></span> <span data-ttu-id="f321f-109">Media Services korumalı içeriği hakları ve DRM çalışma zamanı kullanıcı DRM kayıttan yürüttüğünde uygulanmasını istediğiniz kısıtlamaları yapılandırmanıza olanak tanıyan API'ler de sağlar.</span><span class="sxs-lookup"><span data-stu-id="f321f-109">Media Services also provides APIs that let you configure the rights and restrictions that you want for the DRM runtime to enforce when a user plays back the DRM protected content.</span></span> <span data-ttu-id="f321f-110">Bir kullanıcının korumalı içeriği istediğinde, oynatıcı uygulaması AMS lisans hizmetinden bir lisans ister.</span><span class="sxs-lookup"><span data-stu-id="f321f-110">When a user requests the protected content, the player application will request a license from the AMS license service.</span></span> <span data-ttu-id="f321f-111">(Yetkiliyse) AMS lisans hizmeti lisans oynatıcıya.</span><span class="sxs-lookup"><span data-stu-id="f321f-111">The AMS license service will issue the license to the player (if it is authorized).</span></span> <span data-ttu-id="f321f-112">PlayReady ve Widevine lisansları istemci oynatıcısının içeriğin akış ve şifresini çözmek için kullanılan şifre çözme anahtarını içerir.</span><span class="sxs-lookup"><span data-stu-id="f321f-112">The PlayReady and Widevine licenses contain the decryption key that can be used by the client player to decrypt and stream the content.</span></span>

<span data-ttu-id="f321f-113">Media Services lisans ya da anahtar istekleri yapabilen Kullanıcıları yetkilendirmek, birden çok yöntemini destekler.</span><span class="sxs-lookup"><span data-stu-id="f321f-113">Media Services supports multiple ways of authorizing users who make license or key requests.</span></span> <span data-ttu-id="f321f-114">İçerik anahtarının yetkilendirme ilkesini yapılandırın ve ilkeyi bir veya daha fazla kısıtlamaları olabilir: açık veya belirteç kısıtlama.</span><span class="sxs-lookup"><span data-stu-id="f321f-114">You configure the content key's authorization policy and the policy could have one or more restrictions: open or token restriction.</span></span> <span data-ttu-id="f321f-115">Belirteç kısıtlamalı ilkenin beraberinde bir Güvenli Belirteç Hizmeti (STS) tarafından verilmiş bir belirteç bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f321f-115">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="f321f-116">Media Services, basit Web belirteçleri (SWT) biçimini ve JSON Web Token (JWT) biçimlerindeki belirteçleri destekler.</span><span class="sxs-lookup"><span data-stu-id="f321f-116">Media Services supports tokens in the Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span>

<span data-ttu-id="f321f-117">Aşağıdaki diyagramda, AMS kullanın PlayReady ve/veya Widevine lisansları teslim ancak geri kalan şirket içi sunucularınız ile yapmak için atmanız gereken ana adımları gösterir.</span><span class="sxs-lookup"><span data-stu-id="f321f-117">The following diagram shows the main steps you need to take to use AMS to deliver PlayReady and/or Widevine licenses but do the rest with your on-premises servers.</span></span>

![PlayReady ile koruma](./media/media-services-deliver-keys-and-licenses/media-services-diagram1.png)

## <a name="download-sample"></a><span data-ttu-id="f321f-119">Örnek indirme</span><span class="sxs-lookup"><span data-stu-id="f321f-119">Download sample</span></span>
<span data-ttu-id="f321f-120">Bu makalede açıklanan örneği [buradan](https://github.com/Azure/media-services-dotnet-deliver-drm-licenses) indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f321f-120">You can download the sample described in this article from [here](https://github.com/Azure/media-services-dotnet-deliver-drm-licenses).</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="f321f-121">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f321f-121">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="f321f-122">Geliştirme ortamınızı kurun ve app.config dosyanızı [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md) bölümünde açıklandığı gibi bağlantı bilgileriyle doldurun.</span><span class="sxs-lookup"><span data-stu-id="f321f-122">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="f321f-123">App.config dosyanızda tanımlanan **appSettings**’e aşağıdaki öğeleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f321f-123">Add the following elements to **appSettings** defined in your app.config file:</span></span>

    <span data-ttu-id="f321f-124"><add key="Issuer" value="http://testacs.com"/> <add key="Audience" value="urn:test"/></span><span class="sxs-lookup"><span data-stu-id="f321f-124"><add key="Issuer" value="http://testacs.com"/> <add key="Audience" value="urn:test"/></span></span>

## <a name="net-code-example"></a><span data-ttu-id="f321f-125">.NET kodu örneği</span><span class="sxs-lookup"><span data-stu-id="f321f-125">.NET code example</span></span>

<span data-ttu-id="f321f-126">Aşağıdaki kod örneği, ortak bir içerik anahtarı oluşturun ve PlayReady veya Widevine lisans edinme URL'si almak gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f321f-126">The following code example shows how to create a common content key and get PlayReady or Widevine license acquisition URLs.</span></span> <span data-ttu-id="f321f-127">AMS şu bilgileri alın ve şirket içi sunucunuzu yapılandırmak gereken: **içerik anahtarı**, **anahtarı kimliği**, **lisans edinme URL'si**.</span><span class="sxs-lookup"><span data-stu-id="f321f-127">You need to get the following pieces of information from AMS and configure your on-premises server: **content key**, **key id**, **license acquisition URL**.</span></span> <span data-ttu-id="f321f-128">Şirket içi sunucunuzu yapılandırdıktan sonra kendi akış sunucusundan akış.</span><span class="sxs-lookup"><span data-stu-id="f321f-128">Once you configure your on-premises server, you could stream from your own streaming server.</span></span> <span data-ttu-id="f321f-129">Şifrelenmiş akış noktalarına AMS lisans sunucusunu bu yana, player AMS lisans ister.</span><span class="sxs-lookup"><span data-stu-id="f321f-129">Since the encrypted stream points to AMS license server, your player will request a license from AMS.</span></span> <span data-ttu-id="f321f-130">Belirteç kimlik doğrulamasını seçerseniz, AMS lisans sunucusu HTTPS gönderilen belirteç doğrular ve (geçerli ise) lisans aygıta geri teslim eder.</span><span class="sxs-lookup"><span data-stu-id="f321f-130">If you choose token authentication, the AMS license server will validate the token you sent through HTTPS and (if valid) will deliver the license back to your player.</span></span> <span data-ttu-id="f321f-131">(Kod örneği yalnızca ortak bir içerik anahtarı oluşturun ve PlayReady veya Widevine lisans edinme URL'si almak gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f321f-131">(The code example only shows how to create a common content key and  get PlayReady or Widevine license acquisition URLs.</span></span> <span data-ttu-id="f321f-132">Teslim AES-128 anahtarları istiyorsanız, bir zarf içerik anahtarı oluşturun ve bir anahtar alım URL'sini alma gerekir ve [bu](media-services-protect-with-aes128.md) makalede nasıl yapılacağı gösterilmektedir).</span><span class="sxs-lookup"><span data-stu-id="f321f-132">If you want to delivery AES-128 keys, you need to create an envelope content key and get a key acquisition URL and [this](media-services-protect-with-aes128.md) article shows how to do it).</span></span>

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
            // Read values from the App.config file.
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

                // Print out the key ID and Key in base64 string format
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
                // Associate the content key authorization policy with the content key.
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

                //The PlayReadyLicenseResponseTemplate class represents the template 
                //for the response sent back to the end user. 
                //It contains a field for a custom data string between the license server 
                //and the application (may be useful for custom app logic) 
                //as well as a list of one or more license templates.

                PlayReadyLicenseResponseTemplate responseTemplate =
                    new PlayReadyLicenseResponseTemplate();

                // The PlayReadyLicenseTemplate class represents a license template 
                // for creating PlayReady licenses
                // to be returned to the end users. 
                // It contains the data on the content key in the license 
                // and any rights or restrictions to be 
                // enforced by the PlayReady DRM runtime when using the content key.
                PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();

                // Configure whether the license is persistent 
                // (saved in persistent storage on the client) 
                // or non-persistent (only held in memory while the player is using the license).  
                licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

                // AllowTestDevices controls whether test devices can use the license or not.  
                // If true, the MinimumSecurityLevel property of the license
                // is set to 150.  If false (the default), 
                // the MinimumSecurityLevel property of the license is set to 2000.
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

                // IMPORTANT: These types of restrictions can be very powerful 
                // but can also affect the consumer experience. 
                // If the output protections are configured too restrictive, 
                // the content might be unplayable on some clients. 
                // For more information, see the PlayReady Compliance Rules document.

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="f321f-133">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="f321f-133">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f321f-134">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="f321f-134">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="f321f-135">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="f321f-135">See also</span></span>
[<span data-ttu-id="f321f-136">PlayReady ve/veya Widevine dinamik ortak şifreleme kullanma</span><span class="sxs-lookup"><span data-stu-id="f321f-136">Using PlayReady and/or Widevine Dynamic Common Encryption</span></span>](media-services-protect-with-drm.md)

[<span data-ttu-id="f321f-137">AES-128 dinamik şifreleme ve anahtar teslim hizmeti kullanma</span><span class="sxs-lookup"><span data-stu-id="f321f-137">Using AES-128 Dynamic Encryption and Key Delivery Service</span></span>](media-services-protect-with-aes128.md)

[<span data-ttu-id="f321f-138">Azure Media Services’ta Widevine lisanslarını teslim etmek için iş ortaklarıyla çalışma</span><span class="sxs-lookup"><span data-stu-id="f321f-138">Using partners to deliver Widevine licenses to Azure Media Services</span></span>](media-services-licenses-partner-integration.md)

