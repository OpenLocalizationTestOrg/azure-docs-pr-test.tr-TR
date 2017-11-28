---
title: "aaaUsing Axinom toodeliver Widevine lisansları tooAzure Media Services | Microsoft Docs"
description: "Bu makalede, Azure Media Services (AMS) toodeliver, PlayReady ve Widevine DRMs AMS tarafından dinamik olarak şifrelenmiş bir akış nasıl kullanabileceğinizi açıklar. Medya Hizmetleri PlayReady lisans sunucusundan Hello PlayReady lisans gelir ve Axinom lisans sunucusu tarafından Widevine lisans teslim edilir."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 9c93fa4e-b4da-4774-ab6d-8b12b371631d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: willzhan;Mingfeiy;rajputam;Juliako
ms.openlocfilehash: 2245d9269c30712ef779973ae021c00c76174d0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-axinom-toodeliver-widevine-licenses-tooazure-media-services"></a><span data-ttu-id="dd8fd-104">Axinom toodeliver Widevine lisansları tooAzure Media Services'i kullanma</span><span class="sxs-lookup"><span data-stu-id="dd8fd-104">Using Axinom toodeliver Widevine licenses tooAzure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dd8fd-105">castLabs</span><span class="sxs-lookup"><span data-stu-id="dd8fd-105">castLabs</span></span>](media-services-castlabs-integration.md)
> * [<span data-ttu-id="dd8fd-106">Axinom</span><span class="sxs-lookup"><span data-stu-id="dd8fd-106">Axinom</span></span>](media-services-axinom-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="dd8fd-107">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="dd8fd-107">Overview</span></span>
<span data-ttu-id="dd8fd-108">Azure Media Services (AMS), Google Widevine dinamik koruma ekledi (bkz [Mingfei'nın blogu](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) Ayrıntılar için).</span><span class="sxs-lookup"><span data-stu-id="dd8fd-108">Azure Media Services (AMS) has added Google Widevine dynamic protection (see [Mingfei’s blog](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) for details).</span></span> <span data-ttu-id="dd8fd-109">Ayrıca, Azure Media Player (AMP) Widevine destek da ekledi (bkz [AMP belge](http://amp.azure.net/libs/amp/latest/docs/) Ayrıntılar için).</span><span class="sxs-lookup"><span data-stu-id="dd8fd-109">In addition, Azure Media Player (AMP) has also added Widevine support (see [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details).</span></span> <span data-ttu-id="dd8fd-110">Bu çok-native DRM ile (PlayReady ve Widevine) CENC tarafından korunan tire içeriği akış ana gerçekleştirmek MSE ve EME ile donatılmış modern tarayıcılar açıktır.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-110">This is a major accomplishment in streaming DASH content protected by CENC with multi-native-DRM (PlayReady and Widevine) on modern browsers equipped with MSE and EME.</span></span>

<span data-ttu-id="dd8fd-111">Media Services .NET SDK'sı sürüm 3.5.2'de Hello ile başlayarak, Media Services, tooconfigure Widevine lisans şablonu sağlar ve Widevine lisansları alın.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-111">Starting with hello Media Services .NET SDK version 3.5.2, Media Services enables you tooconfigure Widevine license template and get Widevine licenses.</span></span> <span data-ttu-id="dd8fd-112">Widevine lisansları teslim AMS ortaklarını toohelp aşağıdaki hello de kullanabilirsiniz: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="dd8fd-112">You can also use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="dd8fd-113">Bu makalede nasıl toointegrate ve test Widevine lisans sunucusunu Axinom tarafından yönetilen açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-113">This article describes how toointegrate and test Widevine license server managed by Axinom.</span></span> <span data-ttu-id="dd8fd-114">Özellikle şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="dd8fd-114">Specifically, it covers:</span></span>  

* <span data-ttu-id="dd8fd-115">Dinamik ortak şifreleme çoklu DRM (PlayReady ve Widevine) karşılık gelen lisans edinme URL'ler ile yapılandırılmasını;</span><span class="sxs-lookup"><span data-stu-id="dd8fd-115">Configuring dynamic Common Encryption with multi-DRM (PlayReady and Widevine) with corresponding license acquisition URLs;</span></span>
* <span data-ttu-id="dd8fd-116">JWT belirteci içinde sipariş toomeet hello lisans sunucusu gereksinimleri oluşturmak;</span><span class="sxs-lookup"><span data-stu-id="dd8fd-116">Generating a JWT token in order toomeet hello license server requirements;</span></span>
* <span data-ttu-id="dd8fd-117">Lisans edinme JWT belirteci kimlik doğrulaması ile işleyen Azure Media Player uygulama geliştirme;</span><span class="sxs-lookup"><span data-stu-id="dd8fd-117">Developing Azure Media Player app which handles license acquisition with JWT token authentication;</span></span>

<span data-ttu-id="dd8fd-118">tam sistem hello ve anahtar, anahtar kimliği, anahtar çekirdek, JTW belirteci ve onun talep diyagramı aşağıdaki hello tarafından en iyi şekilde açıklanabilir içeriği akışını hello.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-118">hello complete system and hello flow of content key, key ID, key seed, JTW token and its claims can be best described by hello following diagram.</span></span>

![ÇİZGİ ve CENC](./media/media-services-axinom-integration/media-services-axinom1.png)

## <a name="content-protection"></a><span data-ttu-id="dd8fd-120">Content Protection</span><span class="sxs-lookup"><span data-stu-id="dd8fd-120">Content Protection</span></span>
<span data-ttu-id="dd8fd-121">Dinamik koruma ve anahtar teslim ilkesini yapılandırmak için lütfen Mingfei'nın blogu bakın: [nasıl tooconfigure Widevine paketlemeyi Azure Media Services ile](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).</span><span class="sxs-lookup"><span data-stu-id="dd8fd-121">For configuring dynamic protection and key delivery policy, please see Mingfei’s blog: [How tooconfigure Widevine packaging with Azure Media Services](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).</span></span>

<span data-ttu-id="dd8fd-122">Dinamik CENC koruma hello aşağıdaki her ikisi de sahip akış tire için çoklu DRM ile yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="dd8fd-122">You can configure dynamic CENC protection with multi-DRM for DASH streaming having both of hello following:</span></span>

1. <span data-ttu-id="dd8fd-123">MS Edge ve bir belirteç yetkilendirme kısıtlamaları olabilir IE11, PlayReady koruma.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-123">PlayReady protection for MS Edge and IE11, that could have a token authorization restrictions.</span></span> <span data-ttu-id="dd8fd-124">Merhaba belirteç kısıtlamalı ilkenin tarafından bir güvenli belirteç hizmeti (STS), Azure Active Directory gibi bir belirteç olarak eklenmelidir;</span><span class="sxs-lookup"><span data-stu-id="dd8fd-124">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS), such as Azure Active Directory;</span></span>
2. <span data-ttu-id="dd8fd-125">Widevine koruma Chrome için bunu başka bir STS tarafından verilen belirteci ile belirteci kimlik doğrulamasını isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-125">Widevine protection for Chrome, it can require token authentication with token issued by another STS.</span></span> 

<span data-ttu-id="dd8fd-126">Lütfen bakın [JWT belirteci oluşturma](media-services-axinom-integration.md#jwt-token-generation) bölüm için Axinom'ın Widevine lisans sunucusu neden Azure Active Directory bir STS olarak kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-126">Please see [JWT Token Generation](media-services-axinom-integration.md#jwt-token-generation) section for why Azure Active Directory cannot be used as an STS for Axinom’s Widevine license server.</span></span>

### <a name="considerations"></a><span data-ttu-id="dd8fd-127">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="dd8fd-127">Considerations</span></span>
1. <span data-ttu-id="dd8fd-128">Anahtar teslim hizmeti yapılandırmak için anahtar anahtar çekirdek (8888000000000000000000000000000000000000) ve oluşturulan ya da seçilen anahtar kimliği toogenerate hello içeriğinizi Axinom belirtilen hello kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-128">You must use hello Axinom specified key seed (8888000000000000000000000000000000000000) and your generated or selected key ID toogenerate hello content key for configuring key delivery service.</span></span> <span data-ttu-id="dd8fd-129">Axinom lisans sunucusu tabanlı içerik anahtarı içeren tüm lisanslar vermek hello üzerinde aynı sınama ve üretim için geçerli olan çekirdek anahtar.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-129">Axinom license server will issue all licenses containing content keys based on hello same key seed, which is valid for both testing and production.</span></span>
2. <span data-ttu-id="dd8fd-130">Test hello Widevine lisans edinme URL'si: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense).</span><span class="sxs-lookup"><span data-stu-id="dd8fd-130">hello Widevine license acquisition URL for testing: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense).</span></span> <span data-ttu-id="dd8fd-131">Hem HTTP hem de HTTS izin verilir.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-131">Both HTTP and HTTS are allowed.</span></span>

## <a name="azure-media-player-preparation"></a><span data-ttu-id="dd8fd-132">Azure Media Player hazırlama</span><span class="sxs-lookup"><span data-stu-id="dd8fd-132">Azure Media Player Preparation</span></span>
<span data-ttu-id="dd8fd-133">AMP v1.4.0 dinamik olarak PlayReady ve Widevine DRM ile paketlenmiştir AMS içeriği kayıttan yürütmeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-133">AMP v1.4.0 supports playback of AMS content that is dynamically packaged with both PlayReady and Widevine DRM.</span></span>
<span data-ttu-id="dd8fd-134">Widevine lisans sunucusu belirteci kimlik doğrulaması gerektirmiyorsa, Widevine tarafından korunan bir tire içerik toodo tootest gereksinim duyduğunuz ek bir şey yoktur.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-134">If Widevine license server does not require token authentication, there is nothing additional you need toodo tootest a DASH content protected by Widevine.</span></span> <span data-ttu-id="dd8fd-135">Örneğin, basit bir hello AMP takım sağlar [örnek](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), bu sınır ve IE11 ile PlayReady ve Widevine ile Chrome çalışma burada görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-135">For an example, hello AMP team provides a simple [sample](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), where you can see it working in Edge and IE11 with PlayReady and Chrome with Widevine.</span></span>
<span data-ttu-id="dd8fd-136">Merhaba Widevine lisans sunucusu Axinom tarafından sağlanan JWT belirteci kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-136">hello Widevine license server provided by Axinom requires JWT token authentication.</span></span> <span data-ttu-id="dd8fd-137">Merhaba JWT belirteci lisans isteği bir HTTP üstbilgisi "X-AxDRM-ileti" ile birlikte gönderilen toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-137">hello JWT token needs toobe submitted with license request through an HTTP header “X-AxDRM-Message”.</span></span> <span data-ttu-id="dd8fd-138">Bu amaç için javascript hello web AMP ayar hello kaynağı önce barındırma sayfasında aşağıdaki tooadd hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="dd8fd-138">For this purpose, you need tooadd hello following javascript in hello web page hosting AMP before setting hello source:</span></span>

    <script>AzureHtml5JS.KeySystem.WidevineCustomAuthorizationHeader = "X-AxDRM-Message"</script>

<span data-ttu-id="dd8fd-139">Merhaba rest AMP kod olduğu AMP belge olduğu gibi standart AMP API [burada](http://amp.azure.net/libs/amp/latest/docs/).</span><span class="sxs-lookup"><span data-stu-id="dd8fd-139">hello rest of AMP code is standard AMP API as in AMP document [here](http://amp.azure.net/libs/amp/latest/docs/).</span></span>

<span data-ttu-id="dd8fd-140">Bu hello javascript özel yetkilendirme üst bilgisi hala bir kısa vadeli AMP uzun vadeli yaklaşım yayımlanan hello resmi önce yaklaşımdır ayarı için yukarıdaki unutmayın.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-140">Note that hello above javascript for setting custom authorization header is still a short term approach before hello official long term approach in AMP is released.</span></span>

## <a name="jwt-token-generation"></a><span data-ttu-id="dd8fd-141">JWT belirteci oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd8fd-141">JWT Token Generation</span></span>
<span data-ttu-id="dd8fd-142">Test Axinom Widevine lisans sunucusu JWT belirteci kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-142">Axinom Widevine license server for testing requires JWT token authentication.</span></span> <span data-ttu-id="dd8fd-143">Ayrıca, hello JWT belirteci hello Taleplerde temel veri türü yerine karmaşık nesne türünün biridir.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-143">In addition, one of hello claims in hello JWT token is of a complex object type instead of primitive data type.</span></span>

<span data-ttu-id="dd8fd-144">Ne yazık ki, Azure AD ile ilkel türler yalnızca JWT belirteçleri verebilir.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-144">Unfortunately, Azure AD can only issue JWT tokens with primitive types.</span></span> <span data-ttu-id="dd8fd-145">Benzer şekilde, .NET Framework API (System.IdentityModel.tokens.securitytokenhandler ve JwtPayload) yalnızca tooinput karmaşık nesne türü talepler olarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-145">Similarly, .NET Framework API (System.IdentityModel.Tokens.SecurityTokenHandler and JwtPayload) only allows you tooinput complex object type as claims.</span></span> <span data-ttu-id="dd8fd-146">Ancak, hello talep hala dize olarak serileştirilir.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-146">However, hello claims are still serialized as string.</span></span> <span data-ttu-id="dd8fd-147">Bu nedenle biz herhangi birini hello iki Widevine lisans isteği için oluşturma hello JWT belirteci için kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-147">Therefore we cannot use any of hello two for generating hello JWT token for Widevine license request.</span></span>

<span data-ttu-id="dd8fd-148">John Sheehan'ın [JWT Nuget paketi](https://www.nuget.org/packages/JWT) toouse bu Nuget paketi kalacaklarını şekilde hello gereksinimlerini karşılıyor.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-148">John Sheehan’s [JWT Nuget package](https://www.nuget.org/packages/JWT) meets hello needs so we are going toouse this Nuget package.</span></span>

<span data-ttu-id="dd8fd-149">Merhaba ile oluşturma JWT belirteci için hello kodu Axinom Widevine lisans sunucusu gerektirdiği şekilde test etmek için gereksinim duyduğu talepleri aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="dd8fd-149">Below is hello code for generating JWT token with hello needed claims as required by Axinom Widevine license server for testing:</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.IdentityModel.Tokens;
    using System.IdentityModel.Protocols.WSTrust;
    using System.Security.Claims;

    namespace OpenIdConnectWeb.Utils
    {
        public class JwtUtils
        {
            //using John Sheehan's NuGet JWT library: https://www.nuget.org/packages/JWT/
            public static string CreateJwtSheehan(string symmetricKeyHex, string key_id)
            {
                byte[] symmetricKey = ConvertHexStringToByteArray(symmetricKeyHex);  //hex string toobyte[] Note: Note that hello key is a hex string, however it must be treated as a series of bytes not a string when encoding.

                var payload = new Dictionary<string, object>()
                             {
                                 { "version", 1 },
                                 { "com_key_id", System.Configuration.ConfigurationManager.AppSettings["ax:com_key_id"] },
                                 { "message", new { type = "entitlement_message", key_ids = new string[] { key_id } }  }
                             };

                string token = JWT.JsonWebToken.Encode(payload, symmetricKey, JWT.JwtHashAlgorithm.HS256);

                return token;
            }

            //convert hex string toobyte[]
            public static byte[] ConvertHexStringToByteArray(string hexString)
            {
                if (hexString.Length % 2 != 0)
                {
                    throw new ArgumentException(String.Format(System.Globalization.CultureInfo.InvariantCulture, "hello binary key cannot have an odd number of digits: {0}", hexString));
                }

                byte[] HexAsBytes = new byte[hexString.Length / 2];
                for (int index = 0; index < HexAsBytes.Length; index++)
                {
                    string byteValue = hexString.Substring(index * 2, 2);
                    HexAsBytes[index] = byte.Parse(byteValue, System.Globalization.NumberStyles.HexNumber, System.Globalization.CultureInfo.InvariantCulture);
                }

                return HexAsBytes;
            }

        }  

    }  

<span data-ttu-id="dd8fd-150">Axinom Widevine lisans sunucusu</span><span class="sxs-lookup"><span data-stu-id="dd8fd-150">Axinom Widevine license server</span></span>

    <add key="ax:laurl" value="http://drm-widevine-licensing.axtest.net/AcquireLicense" />
    <add key="ax:com_key_id" value="69e54088-e9e0-4530-8c1a-1eb6dcd0d14e" />
    <add key="ax:com_key" value="4861292d027e269791093327e62ceefdbea489a4c7e5a4974cc904b840fd7c0f" />
    <add key="ax:keyseed" value="8888000000000000000000000000000000000000" />

### <a name="considerations"></a><span data-ttu-id="dd8fd-151">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="dd8fd-151">Considerations</span></span>
1. <span data-ttu-id="dd8fd-152">AMS PlayReady lisans teslimat hizmetinin gerektirir olsa bile "taşıyıcı =" kimlik doğrulama belirtecini önceki, Axinom Widevine lisans sunucusu onu kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-152">Even though AMS PlayReady license delivery service requires “Bearer=” preceding an authentication token, Axinom Widevine license server does not use it.</span></span>
2. <span data-ttu-id="dd8fd-153">Merhaba Axinom iletişimi anahtar imzalama anahtarı olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-153">hello Axinom communication key is used as signing key.</span></span> <span data-ttu-id="dd8fd-154">Ancak, bu bir dize değil bir bayt serisi kodlarken Muamele görmelidir hello anahtara onaltılık dize olmasına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-154">Note that hello key is a hex string, however it must be treated as a series of bytes not a string when encoding.</span></span> <span data-ttu-id="dd8fd-155">Bu ConvertHexStringToByteArray hello yöntemi tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-155">This is achieved by hello method ConvertHexStringToByteArray.</span></span>

## <a name="retrieving-key-id"></a><span data-ttu-id="dd8fd-156">Anahtar kimliği alma</span><span class="sxs-lookup"><span data-stu-id="dd8fd-156">Retrieving Key ID</span></span>
<span data-ttu-id="dd8fd-157">JWT'nin oluşturmak için hello kodda belirteci, anahtar kimliği gerekli olduğunu fark etmiş olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-157">You may have noticed that in hello code for generating a JWT token, key ID is required.</span></span> <span data-ttu-id="dd8fd-158">Merhaba JWT belirteci toobe hazır AMP player yüklemeden önce gerektiğinden, içinde toobe alınan anahtar kimliği gereksinimlerini toogenerate JWT belirteci sipariş.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-158">Since hello JWT token needs toobe ready before loading AMP player, key ID needs toobe retrieved in order toogenerate JWT token.</span></span>

<span data-ttu-id="dd8fd-159">Birden çok yolla tooget tutun anahtarının seyri kimliği</span><span class="sxs-lookup"><span data-stu-id="dd8fd-159">Of course there are multiple ways tooget hold of key ID.</span></span> <span data-ttu-id="dd8fd-160">Örneğin, bir depolayabilir içerik meta veri veritabanındaki birlikte anahtar kimliği.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-160">For example, one may store key ID together with content metadata in a database.</span></span> <span data-ttu-id="dd8fd-161">Veya, alabilirsiniz anahtar tire MPD (medya sunu açıklaması) dosyasından kimliği.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-161">Or you can retrieve key ID from DASH MPD (Media Presentation Description) file.</span></span> <span data-ttu-id="dd8fd-162">Merhaba aşağıdaki hello ikinci kodudur.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-162">hello code below is for hello latter.</span></span>

    //get key_id from DASH MPD
    public static string GetKeyID(string dashUrl)
    {
        if (!dashUrl.EndsWith("(format=mpd-time-csf)"))
        {
            dashUrl += "(format=mpd-time-csf)";
        }

        XPathDocument objXPathDocument = new XPathDocument(dashUrl);
        XPathNavigator objXPathNavigator = objXPathDocument.CreateNavigator();
        XmlNamespaceManager objXmlNamespaceManager = new XmlNamespaceManager(objXPathNavigator.NameTable);
        objXmlNamespaceManager.AddNamespace("",     "urn:mpeg:dash:schema:mpd:2011");
        objXmlNamespaceManager.AddNamespace("ns1",  "urn:mpeg:dash:schema:mpd:2011");
        objXmlNamespaceManager.AddNamespace("cenc", "urn:mpeg:cenc:2013");
        objXmlNamespaceManager.AddNamespace("ms",   "urn:microsoft");
        objXmlNamespaceManager.AddNamespace("mspr", "urn:microsoft:playready");
        objXmlNamespaceManager.AddNamespace("xsi",  "http://www.w3.org/2001/XMLSchema-instance");
        objXmlNamespaceManager.PushScope();

        XPathNodeIterator objXPathNodeIterator;
        objXPathNodeIterator = objXPathNavigator.Select("//ns1:MPD/ns1:Period/ns1:AdaptationSet/ns1:ContentProtection[@value='cenc']", objXmlNamespaceManager);

        string key_id = string.Empty;
        if (objXPathNodeIterator.MoveNext())
        {
            key_id = objXPathNodeIterator.Current.GetAttribute("default_KID", "urn:mpeg:cenc:2013");
        }

        return key_id;
    }

## <a name="summary"></a><span data-ttu-id="dd8fd-163">Özet</span><span class="sxs-lookup"><span data-stu-id="dd8fd-163">Summary</span></span>
<span data-ttu-id="dd8fd-164">Hem Azure medya Hizmetleri içerik koruma, hem de Azure Media Player Widevine destek son eklenmesiyle biz mümkün tooimplement tire, akış + çok DRM native (PlayReady + Widevine) AMS ve Widevine lisans hem PlayReady lisans hizmetiyle Axinom bir sunucudan modern tarayıcılar aşağıdaki hello için:</span><span class="sxs-lookup"><span data-stu-id="dd8fd-164">With latest addition of Widevine support in both Azure Media Services Content Protection and Azure Media Player, we are able tooimplement streaming of DASH + Multi-native-DRM (PlayReady + Widevine) with both PlayReady license service in AMS and Widevine license server from Axinom for hello following modern browsers:</span></span>

* <span data-ttu-id="dd8fd-165">Chrome</span><span class="sxs-lookup"><span data-stu-id="dd8fd-165">Chrome</span></span>
* <span data-ttu-id="dd8fd-166">Windows 10 Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="dd8fd-166">Microsoft Edge on Windows 10</span></span>
* <span data-ttu-id="dd8fd-167">Windows 8.1 ve Windows 10 IE 11</span><span class="sxs-lookup"><span data-stu-id="dd8fd-167">IE 11 on Windows 8.1 and Windows 10</span></span>
* <span data-ttu-id="dd8fd-168">Firefox (Masaüstü) ve Mac (iOS değil) üzerinde Safari Silverlight da desteklenir ve Azure Media Player ile aynı URL hello</span><span class="sxs-lookup"><span data-stu-id="dd8fd-168">Both Firefox (Desktop) and Safari on Mac (not iOS) are also supported via Silverlight and hello same URL with Azure Media Player</span></span>

<span data-ttu-id="dd8fd-169">Merhaba aşağıdaki parametreleri hello Mini çözüm yararlanmayı Axinom Widevine lisans sunucusu gereklidir.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-169">hello following parameters are required in hello mini-solution leveraging Axinom Widevine license server.</span></span> <span data-ttu-id="dd8fd-170">Anahtar dışında kimliği, parametre hello rest kendi Widevine sunucu kurulumu temel alınarak Axinom tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-170">Except for key ID, hello rest of parameters are provided by Axinom based on their Widevine server setup.</span></span>

| <span data-ttu-id="dd8fd-171">Parametre</span><span class="sxs-lookup"><span data-stu-id="dd8fd-171">Parameter</span></span> | <span data-ttu-id="dd8fd-172">Nasıl kullanılır</span><span class="sxs-lookup"><span data-stu-id="dd8fd-172">How it is used</span></span> |
| --- | --- |
| <span data-ttu-id="dd8fd-173">İletişim anahtar kimliği</span><span class="sxs-lookup"><span data-stu-id="dd8fd-173">Communication key ID</span></span> |<span data-ttu-id="dd8fd-174">JWT belirteci hello talep "com_key_id" değeri olarak dahil edilmesi gerekir (bkz [bu](media-services-axinom-integration.md#jwt-token-generation) bölümü).</span><span class="sxs-lookup"><span data-stu-id="dd8fd-174">Must be included as value of hello claim "com_key_id" in JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="dd8fd-175">İletişim anahtarı</span><span class="sxs-lookup"><span data-stu-id="dd8fd-175">Communication key</span></span> |<span data-ttu-id="dd8fd-176">JWT belirtecinin imzalama anahtarı hello olarak kullanılmalıdır (bkz [bu](media-services-axinom-integration.md#jwt-token-generation) bölümü).</span><span class="sxs-lookup"><span data-stu-id="dd8fd-176">Must be used as hello signing key of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="dd8fd-177">Anahtar çekirdek</span><span class="sxs-lookup"><span data-stu-id="dd8fd-177">Key seed</span></span> |<span data-ttu-id="dd8fd-178">Kullanılan toogenerate içerik anahtarı herhangi biriyle içerik verilmelidir anahtar kimliği (bkz [bu](media-services-axinom-integration.md#content-protection) bölümü).</span><span class="sxs-lookup"><span data-stu-id="dd8fd-178">Must be used toogenerate content key with any given content key ID (see  [this](media-services-axinom-integration.md#content-protection) section).</span></span> |
| <span data-ttu-id="dd8fd-179">Widevine lisans edinme URL'si</span><span class="sxs-lookup"><span data-stu-id="dd8fd-179">Widevine License acquisition URL</span></span> |<span data-ttu-id="dd8fd-180">TİRE akış için varlık teslim ilkesini yapılandırma kullanılması gerekir (bkz [bu](media-services-axinom-integration.md#content-protection) bölümü).</span><span class="sxs-lookup"><span data-stu-id="dd8fd-180">Must be used in configuring asset delivery policy for DASH streaming (see  [this](media-services-axinom-integration.md#content-protection) section ).</span></span> |
| <span data-ttu-id="dd8fd-181">İçerik anahtarı kimliği</span><span class="sxs-lookup"><span data-stu-id="dd8fd-181">Content Key ID</span></span> |<span data-ttu-id="dd8fd-182">JWT belirteci yetkilendirme ileti talep hello değerinin bir parçası olarak dahil olması gerekir (bkz [bu](media-services-axinom-integration.md#jwt-token-generation) bölümü).</span><span class="sxs-lookup"><span data-stu-id="dd8fd-182">Must be included as part of hello value of Entitlement Message claim of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |

## <a name="media-services-learning-paths"></a><span data-ttu-id="dd8fd-183">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="dd8fd-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="dd8fd-184">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="dd8fd-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="dd8fd-185">İlgili kaynaklar</span><span class="sxs-lookup"><span data-stu-id="dd8fd-185">Acknowledgments</span></span>
<span data-ttu-id="dd8fd-186">Bu belge oluşturma doğrultusunda katkıda bulunan kişiler aşağıdaki tooacknowledge hello isteriz: Axinom, Kristjan Jõgi, Mingfei Yan ve Amit Rajput.</span><span class="sxs-lookup"><span data-stu-id="dd8fd-186">We would like tooacknowledge hello following people who contributed towards creating this document: Kristjan Jõgi of Axinom, Mingfei Yan, and Amit Rajput.</span></span>

