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
# <a name="using-axinom-toodeliver-widevine-licenses-tooazure-media-services"></a>Axinom toodeliver Widevine lisansları tooAzure Media Services'i kullanma
> [!div class="op_single_selector"]
> * [castLabs](media-services-castlabs-integration.md)
> * [Axinom](media-services-axinom-integration.md)
> 
> 

## <a name="overview"></a>Genel Bakış
Azure Media Services (AMS), Google Widevine dinamik koruma ekledi (bkz [Mingfei'nın blogu](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) Ayrıntılar için). Ayrıca, Azure Media Player (AMP) Widevine destek da ekledi (bkz [AMP belge](http://amp.azure.net/libs/amp/latest/docs/) Ayrıntılar için). Bu çok-native DRM ile (PlayReady ve Widevine) CENC tarafından korunan tire içeriği akış ana gerçekleştirmek MSE ve EME ile donatılmış modern tarayıcılar açıktır.

Media Services .NET SDK'sı sürüm 3.5.2'de Hello ile başlayarak, Media Services, tooconfigure Widevine lisans şablonu sağlar ve Widevine lisansları alın. Widevine lisansları teslim AMS ortaklarını toohelp aşağıdaki hello de kullanabilirsiniz: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).

Bu makalede nasıl toointegrate ve test Widevine lisans sunucusunu Axinom tarafından yönetilen açıklanmaktadır. Özellikle şunları içerir:  

* Dinamik ortak şifreleme çoklu DRM (PlayReady ve Widevine) karşılık gelen lisans edinme URL'ler ile yapılandırılmasını;
* JWT belirteci içinde sipariş toomeet hello lisans sunucusu gereksinimleri oluşturmak;
* Lisans edinme JWT belirteci kimlik doğrulaması ile işleyen Azure Media Player uygulama geliştirme;

tam sistem hello ve anahtar, anahtar kimliği, anahtar çekirdek, JTW belirteci ve onun talep diyagramı aşağıdaki hello tarafından en iyi şekilde açıklanabilir içeriği akışını hello.

![ÇİZGİ ve CENC](./media/media-services-axinom-integration/media-services-axinom1.png)

## <a name="content-protection"></a>Content Protection
Dinamik koruma ve anahtar teslim ilkesini yapılandırmak için lütfen Mingfei'nın blogu bakın: [nasıl tooconfigure Widevine paketlemeyi Azure Media Services ile](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).

Dinamik CENC koruma hello aşağıdaki her ikisi de sahip akış tire için çoklu DRM ile yapılandırabilirsiniz:

1. MS Edge ve bir belirteç yetkilendirme kısıtlamaları olabilir IE11, PlayReady koruma. Merhaba belirteç kısıtlamalı ilkenin tarafından bir güvenli belirteç hizmeti (STS), Azure Active Directory gibi bir belirteç olarak eklenmelidir;
2. Widevine koruma Chrome için bunu başka bir STS tarafından verilen belirteci ile belirteci kimlik doğrulamasını isteyebilirsiniz. 

Lütfen bakın [JWT belirteci oluşturma](media-services-axinom-integration.md#jwt-token-generation) bölüm için Axinom'ın Widevine lisans sunucusu neden Azure Active Directory bir STS olarak kullanılamaz.

### <a name="considerations"></a>Dikkat edilmesi gerekenler
1. Anahtar teslim hizmeti yapılandırmak için anahtar anahtar çekirdek (8888000000000000000000000000000000000000) ve oluşturulan ya da seçilen anahtar kimliği toogenerate hello içeriğinizi Axinom belirtilen hello kullanmanız gerekir. Axinom lisans sunucusu tabanlı içerik anahtarı içeren tüm lisanslar vermek hello üzerinde aynı sınama ve üretim için geçerli olan çekirdek anahtar.
2. Test hello Widevine lisans edinme URL'si: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense). Hem HTTP hem de HTTS izin verilir.

## <a name="azure-media-player-preparation"></a>Azure Media Player hazırlama
AMP v1.4.0 dinamik olarak PlayReady ve Widevine DRM ile paketlenmiştir AMS içeriği kayıttan yürütmeyi destekler.
Widevine lisans sunucusu belirteci kimlik doğrulaması gerektirmiyorsa, Widevine tarafından korunan bir tire içerik toodo tootest gereksinim duyduğunuz ek bir şey yoktur. Örneğin, basit bir hello AMP takım sağlar [örnek](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), bu sınır ve IE11 ile PlayReady ve Widevine ile Chrome çalışma burada görebilirsiniz.
Merhaba Widevine lisans sunucusu Axinom tarafından sağlanan JWT belirteci kimlik doğrulaması gerektirir. Merhaba JWT belirteci lisans isteği bir HTTP üstbilgisi "X-AxDRM-ileti" ile birlikte gönderilen toobe gerekir. Bu amaç için javascript hello web AMP ayar hello kaynağı önce barındırma sayfasında aşağıdaki tooadd hello gerekir:

    <script>AzureHtml5JS.KeySystem.WidevineCustomAuthorizationHeader = "X-AxDRM-Message"</script>

Merhaba rest AMP kod olduğu AMP belge olduğu gibi standart AMP API [burada](http://amp.azure.net/libs/amp/latest/docs/).

Bu hello javascript özel yetkilendirme üst bilgisi hala bir kısa vadeli AMP uzun vadeli yaklaşım yayımlanan hello resmi önce yaklaşımdır ayarı için yukarıdaki unutmayın.

## <a name="jwt-token-generation"></a>JWT belirteci oluşturma
Test Axinom Widevine lisans sunucusu JWT belirteci kimlik doğrulaması gerektirir. Ayrıca, hello JWT belirteci hello Taleplerde temel veri türü yerine karmaşık nesne türünün biridir.

Ne yazık ki, Azure AD ile ilkel türler yalnızca JWT belirteçleri verebilir. Benzer şekilde, .NET Framework API (System.IdentityModel.tokens.securitytokenhandler ve JwtPayload) yalnızca tooinput karmaşık nesne türü talepler olarak sağlar. Ancak, hello talep hala dize olarak serileştirilir. Bu nedenle biz herhangi birini hello iki Widevine lisans isteği için oluşturma hello JWT belirteci için kullanamazsınız.

John Sheehan'ın [JWT Nuget paketi](https://www.nuget.org/packages/JWT) toouse bu Nuget paketi kalacaklarını şekilde hello gereksinimlerini karşılıyor.

Merhaba ile oluşturma JWT belirteci için hello kodu Axinom Widevine lisans sunucusu gerektirdiği şekilde test etmek için gereksinim duyduğu talepleri aşağıdadır:

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

Axinom Widevine lisans sunucusu

    <add key="ax:laurl" value="http://drm-widevine-licensing.axtest.net/AcquireLicense" />
    <add key="ax:com_key_id" value="69e54088-e9e0-4530-8c1a-1eb6dcd0d14e" />
    <add key="ax:com_key" value="4861292d027e269791093327e62ceefdbea489a4c7e5a4974cc904b840fd7c0f" />
    <add key="ax:keyseed" value="8888000000000000000000000000000000000000" />

### <a name="considerations"></a>Dikkat edilmesi gerekenler
1. AMS PlayReady lisans teslimat hizmetinin gerektirir olsa bile "taşıyıcı =" kimlik doğrulama belirtecini önceki, Axinom Widevine lisans sunucusu onu kullanmaz.
2. Merhaba Axinom iletişimi anahtar imzalama anahtarı olarak kullanılır. Ancak, bu bir dize değil bir bayt serisi kodlarken Muamele görmelidir hello anahtara onaltılık dize olmasına dikkat edin. Bu ConvertHexStringToByteArray hello yöntemi tarafından sağlanır.

## <a name="retrieving-key-id"></a>Anahtar kimliği alma
JWT'nin oluşturmak için hello kodda belirteci, anahtar kimliği gerekli olduğunu fark etmiş olabilirsiniz. Merhaba JWT belirteci toobe hazır AMP player yüklemeden önce gerektiğinden, içinde toobe alınan anahtar kimliği gereksinimlerini toogenerate JWT belirteci sipariş.

Birden çok yolla tooget tutun anahtarının seyri kimliği Örneğin, bir depolayabilir içerik meta veri veritabanındaki birlikte anahtar kimliği. Veya, alabilirsiniz anahtar tire MPD (medya sunu açıklaması) dosyasından kimliği. Merhaba aşağıdaki hello ikinci kodudur.

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

## <a name="summary"></a>Özet
Hem Azure medya Hizmetleri içerik koruma, hem de Azure Media Player Widevine destek son eklenmesiyle biz mümkün tooimplement tire, akış + çok DRM native (PlayReady + Widevine) AMS ve Widevine lisans hem PlayReady lisans hizmetiyle Axinom bir sunucudan modern tarayıcılar aşağıdaki hello için:

* Chrome
* Windows 10 Microsoft Edge
* Windows 8.1 ve Windows 10 IE 11
* Firefox (Masaüstü) ve Mac (iOS değil) üzerinde Safari Silverlight da desteklenir ve Azure Media Player ile aynı URL hello

Merhaba aşağıdaki parametreleri hello Mini çözüm yararlanmayı Axinom Widevine lisans sunucusu gereklidir. Anahtar dışında kimliği, parametre hello rest kendi Widevine sunucu kurulumu temel alınarak Axinom tarafından sağlanır.

| Parametre | Nasıl kullanılır |
| --- | --- |
| İletişim anahtar kimliği |JWT belirteci hello talep "com_key_id" değeri olarak dahil edilmesi gerekir (bkz [bu](media-services-axinom-integration.md#jwt-token-generation) bölümü). |
| İletişim anahtarı |JWT belirtecinin imzalama anahtarı hello olarak kullanılmalıdır (bkz [bu](media-services-axinom-integration.md#jwt-token-generation) bölümü). |
| Anahtar çekirdek |Kullanılan toogenerate içerik anahtarı herhangi biriyle içerik verilmelidir anahtar kimliği (bkz [bu](media-services-axinom-integration.md#content-protection) bölümü). |
| Widevine lisans edinme URL'si |TİRE akış için varlık teslim ilkesini yapılandırma kullanılması gerekir (bkz [bu](media-services-axinom-integration.md#content-protection) bölümü). |
| İçerik anahtarı kimliği |JWT belirteci yetkilendirme ileti talep hello değerinin bir parçası olarak dahil olması gerekir (bkz [bu](media-services-axinom-integration.md#jwt-token-generation) bölümü). |

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a>İlgili kaynaklar
Bu belge oluşturma doğrultusunda katkıda bulunan kişiler aşağıdaki tooacknowledge hello isteriz: Axinom, Kristjan Jõgi, Mingfei Yan ve Amit Rajput.

