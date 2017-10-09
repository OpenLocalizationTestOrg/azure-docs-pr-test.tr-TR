---
title: "aaaUsing PlayReady ve/veya Widevine dinamik ortak şifreleme | Microsoft Docs"
description: "Microsoft Azure Media Services, Microsoft PlayReady DRM korumalı, toodeliver MPEG-DASH, kesintisiz akış ve Http canlı akış (HLS) akışlar sağlar. Ayrıca, Widevine DRM ile şifrelenmiş DASH toodelivery sağlar. Bu konu, toodynamically nasıl şifrelemek PlayReady ve Widevine DRM ile gösterir."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 548d1a12-e2cb-45fe-9307-4ec0320567a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 0475e6ec80dcf39eb4e5c4ad4d17f821502951bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-playready-andor-widevine-dynamic-common-encryption"></a>PlayReady ve/veya Widevine dinamik ortak şifreleme kullanma

> [!div class="op_single_selector"]
> * [.NET](media-services-protect-with-drm.md)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
>
>

Microsoft Azure Media Services sağlar toodeliver MPEG-DASH, kesintisiz akış ve HTTP canlı akış (HLS) akışlar ile korunan [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). Ayrıca, Widevine DRM lisansına sahip toodeliver şifrelenmiş DASH akışları sağlar. PlayReady ve Widevine, ortak şifreleme (ISO/IEC 23001-7 CENC) belirtimi hello şifrelenir. Kullanabileceğiniz [AMS .NET SDK'sı](https://www.nuget.org/packages/windowsazure.mediaservices/) (3.5.1 hello sürümünden başlayarak) veya API tooconfigure, AssetDeliveryConfiguration toouse Widevine getirin.

Media Services, PlayReady ve Widevine DRM lisansları teslim etmek üzere bir hizmet sunar. Media Services de hello haklarını yapılandırmanıza olanak tanıyan API'ler sağlar ve hello PlayReady veya Widevine DRM çalışma zamanı tooenforce için bir kullanıcı istediğiniz kısıtlamaları oynar geri korumalı içeriği. Kullanıcı DRM korumalı bir içerik istediğinde, Merhaba oynatıcı uygulaması hello AMS lisans hizmetinden bir lisans ister. yetkili olup olmadığını hello AMS lisans hizmeti bir lisans toohello oynatıcı gönderirsiniz. PlayReady veya Widevine lisans hello istemci player toodecrypt ve akış Merhaba içeriğine tarafından kullanılan hello şifre çözme anahtarını içerir.

Widevine lisansları teslim AMS ortaklarını toohelp aşağıdaki hello de kullanabilirsiniz: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/). Daha fazla bilgi için [Axinom](media-services-axinom-integration.md) ve [castLabs](media-services-castlabs-integration.md) ile tümleştirme makalelerine bakın.

Media Services, anahtar isteğinde bulunan kullanıcıları yetkilendirmenin birden çok yöntemini destekler. Merhaba içerik anahtarı yetkilendirme ilkesini bir veya daha fazla yetkilendirme kısıtlamaları olabilir: açık veya belirteç kısıtlama. Merhaba belirteç kısıtlamalı ilkenin, bir güvenli belirteç hizmeti (STS) tarafından verilmiş bir belirteç tarafından eklenmelidir. Media Services hello belirteçleri destekler [basit Web belirteçleri](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) biçimi ve [JSON Web belirteci](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) biçimi. Daha fazla bilgi için yapılandırma hello içerik anahtarının yetkilendirme ilkesini bakın.

tootake avantajı dinamik şifrelenmesi toohave Çoklu bit hızlı MP4 dosyası ya da Çoklu bit hızlı kesintisiz akış kaynak dosyası içeren bir varlık gerekir. (Bu konunun ilerleyen bölümlerinde açıklanan) hello varlık için tooconfigure hello teslim ilkeleri de gerekir. Ardından, akış URL'si hello belirtilen hello biçime bağlı olarak, hello isteğe bağlı Akış sunucusu bu hello akış seçmiş olduğunuz hello protokolde teslim güvence altına alır. Sonuç olarak, yalnızca toostore gerekir ve tek bir depolama biçiminde ve Media Services hello dosyaları ödeme hello her istemciden gelen isteklere göre uygun HTTP yanıtı derler ve.

Bu konuda benzeri PlayReady ve Widevine gibi birden çok DRM ile korunan medya teslim uygulamalar üzerinde çalışmak yararlı toodevelopers olacaktır. Merhaba konu nasıl tooconfigure hello PlayReady lisans teslimat hizmetinin Yetkilendirme İlkeleri ile yalnızca yetkili istemcilerin PlayReady veya Widevine lisansları alabilmesini olduğunu gösterir. Ayrıca gösterir nasıl toouse dinamik şifrelemenin PlayReady veya Widevine DRM tire üzerinden.

>[!NOTE]
>AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu. İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu. 

## <a name="download-sample"></a>Örnek indirme
Bu makalede açıklanan hello örnek indirebilirsiniz [burada](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).

## <a name="configuring-dynamic-common-encryption-and-drm-license-delivery-services"></a>Dinamik Ortak Şifreleme ve DRM Lisans Teslimat Hizmetlerini Yapılandırma

Merhaba, hello Media Services lisans teslimat hizmeti ve dinamik şifreleme kullanarak PlayReady ile varlıklarınızı korurken tooperform gerekir genel adımlar verilmiştir.

1. Bir varlık oluşturun ve dosyaları hello varlığa yükleyin.
2. Merhaba varlık içeren hello dosya toohello Uyarlamalı bit hızı MP4 kümesine kodlayın.
3. Bir içerik anahtarı oluşturup kodlanmış hello varlıkla ilişkilendirin. Media Services'de hello içerik anahtarı hello varlığın şifreleme anahtarını içerir.
4. Merhaba içerik anahtarının yetkilendirme ilkesini yapılandırın. Merhaba içerik anahtarı yetkilendirme ilkesinin tarafınızdan yapılandırılması ve hello içerik anahtar toobe teslim toohello istemcisi için sırayla hello istemci tarafından karşılanır.

    Merhaba içerik anahtarı yetkilendirme ilkesini oluştururken toospecify hello aşağıdaki gerekir: teslim yöntemi (PlayReady veya Widevine), kısıtlamalar (açık veya belirteç) ve başlangıç anahtarı nasıl teslim edildiğini tanımlayan bilgileri belirli toohello anahtar teslim türüne toohello istemci ([PlayReady](media-services-playready-license-template-overview.md) veya [Widevine](media-services-widevine-license-template-overview.md) lisans şablonu).

5. Bir varlık için Hello teslim ilkesini yapılandırın. Merhaba teslim ilkesi yapılandırması içerir: teslim Protokolü (örneğin, MPEG DASH, HLS, kesintisiz akış veya tümü), hello dinamik şifreleme (örneğin, ortak şifreleme), PlayReady veya Widevine lisans edinme URL'si.

    Merhaba üzerinde farklı ilke tooeach Protokolü uygulayabilir aynı varlık. Örneğin, PlayReady şifreleme tooSmooth/DASH ve AES zarfı tooHLS uygulayabilirsiniz. Bir teslim ilkesinde tanımlanmayan tüm protokollerin (örneğin, yalnızca hello protokol olarak HLS belirten tek bir ilke ekliyorsunuz) akışla aktarılması engellenir. Merhaba özel durum toothis hiç tanımlanmış hiçbir varlık teslim ilkesini varsa ' dir. Ardından, tüm protokoller hello Temizle izin verilir.

6. Bir OnDemand Bulucu sipariş tooget bir akış URL'si oluşturun.

Hello hello konunun sonunda eksiksiz bir .NET örneği bulabilirsiniz.

Görüntü aşağıdaki hello yukarıda açıklanan hello akışı gösterilmektedir. Burada hello belirteci kimlik doğrulaması için kullanılır.

![PlayReady ile koruma](./media/media-services-content-protection-overview/media-services-content-protection-with-drm.png)

Bu konunun geri kalanında Hello ayrıntılı açıklamalar, kod örnekleri ve nasıl tooachieve hello yukarıda açıklanan görevleri göster bağlantılar tootopics sağlar.

## <a name="current-limitations"></a>Geçerli sınırlamalar
Eklemek veya bir varlık teslim ilkesini güncelleştirmek, hello ilişkili Bulucuyu (varsa) silin ve yeni bir Bulucu oluşturmanız gerekir.

Azure Media Services aracılığıyla Widevine ile şifrelerken sınırlama: Şu anda, birden çok içerik anahtarı desteklenmemektedir.

## <a name="create-an-asset-and-upload-files-into-hello-asset"></a>Bir varlık oluşturun ve dosyaları hello varlığa yükleyin
Sipariş toomanage kodlamak ve videolarınızı, akış içeriğinizi önce Microsoft Azure Media Services'e yüklemeniz gerekir. Yüklenmesinin ardından içeriğiniz daha fazla işleme ve akış hello bulutta güvenli bir şekilde depolanır.

Ayrıntılı bilgi için bkz. [Media Services hesabına dosya yükleme](media-services-dotnet-upload-files.md).

## <a name="encode-hello-asset-containing-hello-file-toohello-adaptive-bitrate-mp4-set"></a>Merhaba varlık içeren hello dosya toohello Uyarlamalı bit hızı MP4 kümesine kodlayın
Dinamik şifreleme ile tek ihtiyacınız olan toocreate Çoklu bit hızlı MP4 dosyası ya da Çoklu bit hızlı kesintisiz akış kaynak dosyası içeren bir varlık. Merhaba hello bildiriminde belirtilen biçime bağlı olarak ve istek parçalara, hello isteğe bağlı Akış sunucusu, hello akış seçmiş olduğunuz hello protokolde almanızı sağlar. Sonuç olarak, yalnızca toostore gerekir ve tek bir depolama biçiminde ve Media Services hizmeti hello dosyaları ödeme hello istemciden gelen isteklere göre uygun yanıtı derler ve. Daha fazla bilgi için bkz: Merhaba [dinamik paketlemeye genel bakış](media-services-dynamic-packaging-overview.md) konu.

Yönergeler için tooencode, bkz: [nasıl tooencode medya Kodlayıcı standart kullanarak bir varlık](media-services-dotnet-encode-with-media-encoder-standard.md).

## <a id="create_contentkey"></a>Bir içerik anahtarı oluşturup kodlanmış hello varlıkla ilişkilendirme
Media Services'de hello içerik anahtarı tooencrypt bir varlık istediğiniz başlangıç anahtarı içeren ile.

Ayrıntılı bilgi için bkz. [İçerik anahtarı oluşturma](media-services-dotnet-create-contentkey.md).

## <a id="configure_key_auth_policy"></a>Merhaba içerik anahtarının yetkilendirme ilkesini yapılandırın
Media Services, anahtar isteğinde bulunan kullanıcıların kimlik doğrulamasını yapmanın birden çok yöntemini destekler. Merhaba içerik anahtarı yetkilendirme ilkesinin tarafınızdan yapılandırılması ve hello anahtar toobe toohello istemci teslim sırayla hello istemci (oynatıcı) tarafından karşılanır. Merhaba içerik anahtarı yetkilendirme ilkesini bir veya daha fazla yetkilendirme kısıtlamaları olabilir: açık veya belirteç kısıtlama.

Ayrıntılı bilgi için bkz. [İçerik Anahtarı Yetkilendirme İlkesini Yapılandırma](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).

## <a id="configure_asset_delivery_policy"></a>Varlık teslim ilkesini yapılandırma
Varlığınıza Hello teslim ilkesini yapılandırın. Varlık teslim ilkesi yapılandırması hello bazı şeyleri içerir:

* Merhaba DRM lisans edinme URL'si.
* Merhaba varlık teslim Protokolü (örneğin, MPEG DASH, HLS, kesintisiz akış veya tümü).
* (Bu durumda, ortak şifreleme) dinamik şifreleme türü Hello.

Ayrıntılı bilgi için bkz. [Varlık teslim ilkesini yapılandırma](media-services-rest-configure-asset-delivery-policy.md).

## <a id="create_locator"></a>Bir OnDemand Bulucu sipariş tooget bir akış URL'si içinde akış oluşturma
Kullanıcı URL'si kesintisiz, DASH veya HLS akış hello ile tooprovide gerekir.

> [!NOTE]
> Varlığınızın teslim ilkesini ekler veya güncelleştirirseniz, mevcut bulucuyu (varsa) silip yeni bir bulucu oluşturmanız gerekir.
>
>

Yönergeler için nasıl toopublish bir varlık ve yapı bir akış URL'si bkz [akış URL'si oluşturma](media-services-deliver-streaming-content.md).

## <a name="get-a-test-token"></a>Test belirteci alma
Merhaba hello anahtar yetkilendirme ilkesi için kullanılan belirteç kısıtlamasına dayalı bir test belirteci alın.

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string.
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);


Merhaba kullanabilirsiniz [AMS Oynatıcısı](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest akışınızı.

## <a name="create-and-configure-a-visual-studio-project"></a>Visual Studio projesi oluşturup yapılandırma

1. Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md). 
2. Öğeleri çok aşağıdaki hello eklemek**appSettings** app.config dosyasında tanımlanan:

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a>Örnek

Merhaba aşağıdaki örnek, .net için Azure Media Services SDK'sı sunulan işlevini gösterir-(özellikle hello özelliği toodefine bir Widevine lisans şablonu ve Azure Media Services'den Widevine lisansı isteme) sürüm 3.5.2'de.

Bu bölümde gösterilen hello koduyla Hello kodu Program.cs dosyanızdaki üzerine.

>[!NOTE]
>Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için). Merhaba kullanması gereken her zaman kullanıyorsanız, aynı ilke kimliği hello aynı gün / erişim izinlerini, örneğin, uzun bir süre (karşıya yükleme olmayan ilkeleri) yerinde hedeflenen tooremain olan bulucular ilkeleri. Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.

Emin tooupdate değişkenleri, giriş dosyalarınızın bulunduğu toopoint toofolders olun.

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.Widevine;
    using Newtonsoft.Json;

    namespace DynamicEncryptionWithDRM
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

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            bool tokenRestriction = false;
            string tokenTemplateString = null;

            IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
            Console.WriteLine("Uploaded asset: {0}", asset.Id);

            IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
            Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

            IContentKey key = CreateCommonTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("PlayReady License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense));
            Console.WriteLine();

            if (tokenRestriction)
            tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
            else
            AddOpenAuthorizationPolicy(key);

            Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
            Console.WriteLine();

            CreateAssetDeliveryPolicy(encodedAsset, key);
            Console.WriteLine("Created asset delivery policy. \n");
            Console.WriteLine();

            if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
            {
            // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
            // back into a TokenRestrictionTemplate class instance.
            TokenRestrictionTemplate tokenTemplate =
                TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

            // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello http://amsplayer.azurewebsites.net/azuremediaplayer.html player tootest streams.
            // Note that DASH works on IE 11 (via PlayReady), Edge (via PlayReady), Chrome (via Widevine).

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted DASH URL: {0}/manifest(format=mpd-time-csf)", url);

            Console.ReadLine();
        }

        static public IAsset UploadFileAndCreateAsset(string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
            Console.WriteLine("File does not exist.");
            return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
        {
            var encodingPreset = "Adaptive Streaming";

            IJob job = _context.Jobs.Create(String.Format("Encoding into Mp4 {0} too{1}",
                        inputAsset.Name,
                        encodingPreset));

            var mediaProcessors =
            _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

            var latestMediaProcessor =
            mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

            ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
            encodeTask.InputAssets.Add(inputAsset);
            encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset), AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }


        static public IContentKey CreateCommonTypeContentKey(IAsset asset)
        {

            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryption);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }

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

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
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

        private static string ConfigureWidevineLicenseTemplate()
        {
            var template = new WidevineMessage
            {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                    new ContentKeySpecs
                    {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
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
                    {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl, widevineUrl.ToString()}

            };

            // In this case we only specify Dash streaming protocol in hello delivery policy,
            // All other protocols will be blocked from streaming.
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }

        /// <summary>
        /// Gets hello streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator toohello streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL toohello manifest file.
            return originLocator.Path + assetFile.Name;
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
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


## <a name="next-step"></a>Sonraki adım
Media Services öğrenme yollarını gözden geçirin.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Ayrıca bkz.
[Çoklu DRM ve Access Control ile CENC](media-services-cenc-with-multidrm-access-control.md)

[AMS ile Widevine paketlemeyi yapılandırma](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)

[Azure Media Services’ta Google Widevine lisans teslim hizmetleri ile tanışın](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/)
