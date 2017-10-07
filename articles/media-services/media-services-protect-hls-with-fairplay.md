---
title: "aaaProtect HLS içerik Microsoft PlayReady veya Apple FairPlay - Azure ile | Microsoft Docs"
description: "Bu konu genel bir bakış sağlar ve nasıl toouse Azure Media Services toodynamically şifrelemek Apple FairPlay, HTTP canlı akışı (HLS) içeriğinizle gösterir. Aynı zamanda, nasıl toouse hello Media Services lisans teslimat hizmeti toodeliver FairPlay lisansları tooclients gösterir."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7c3b35d9-1269-4c83-8c91-490ae65b0817
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 91ca451e3e7bf0da1d74dac4c99180f08f39e4ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a>Apple FairPlay veya Microsoft PlayReady ile içerik, HLS koruma
Toodynamically şifrelemek HTTP canlı akışı (HLS) içeriğinizi biçimleri aşağıdaki hello kullanarak azure Media Services etkinleştirir:  

* **AES-128 Zarf şifresiz anahtar**

    Merhaba tüm öbek hello kullanılarak şifrelenir **AES-128 CBC** modu. Merhaba akış Hello şifrelerinin iOS ve OS X oyuncu tarafından yerel olarak desteklenir. Daha fazla bilgi için bkz: [AES-128 kullanarak dinamik şifreleme ve anahtar teslim hizmeti](media-services-protect-with-aes128.md).
* **Apple FairPlay**

    hello tek tek video ve ses örnekleri hello kullanarak şifrelenir **AES-128 CBC** modu. **FairPlay akış** (FPS), iOS ve Apple TV yerel desteğiyle hello cihaz işletim sistemlerinin bütünleştirilmiştir. OS X üzerinde Safari hello şifrelenmiş medya Uzantıları (EME) arabirimi desteği kullanarak FPS sağlar.
* **Microsoft PlayReady**

Merhaba aşağıdaki resimde gösterilmiştir hello **HLS + FairPlay veya PlayReady dinamik şifreleme** iş akışı.

![Dinamik şifreleme iş akışı diyagramı](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

Bu konuda nasıl toouse Media Services toodynamically şifrelemek HLS içeriğinizi Apple FairPlay ile gösterilir. Aynı zamanda, nasıl toouse hello Media Services lisans teslimat hizmeti toodeliver FairPlay lisansları tooclients gösterir.

> [!NOTE]
> Ayrıca tooencrypt, HLS PlayReady ile içerik isterseniz, toocreate ortak bir içerik anahtarı gerekir ve Varlığınızı ile ilişkilendirin. Ayrıca tooconfigure hello içerik anahtarının yetkilendirme ilkesini açıklandığı gibi gerekir [dinamik ortak şifreleme kullanarak PlayReady](media-services-protect-with-drm.md).
>
>

## <a name="requirements-and-considerations"></a>Gereksinimleri ve konular

Merhaba HLS şifrelenmiş Media Services toodeliver FairPlay ve toodeliver FairPlay lisansları ile kullanırken gerekli şunlardır:

  * Bir Azure hesabı. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
  * Bir Media Services hesabı. toocreate biri bkz [hello Azure portal kullanarak bir Azure Media Services hesabı oluşturma](media-services-portal-create-account.md).
  * İle kaydolmak [Apple geliştirme programı](https://developer.apple.com/).
  * Apple gerektirir hello içerik sahibi tooobtain hello [dağıtım paketi](https://developer.apple.com/contact/fps/). Media Services ile anahtar güvenlik modülü (KSM) zaten uygulanan ve hello son FPS paket isteyen durumu. Son FPS toogenerate sertifika paketini ve elde hello'ndaki yönergeleri hello uygulama gizli anahtarı (İSTEYİN) vardır. ASK tooconfigure FairPlay kullanın.
  * Azure Media Services .NET SDK sürümü **3.6.0** veya sonraki bir sürümü.

Media Services anahtar teslim tarafında şeyler aşağıdaki hello ayarlamanız gerekir:

  * **Uygulama sertifika (AC)**: hello özel anahtarı içeren bir .pfx dosyası budur. Bu dosyayı oluşturmak ve bir parolayla şifreleyin.

       Bir anahtar teslim İlkesi yapılandırdığınızda, o parola ve hello .pfx dosyasını Base64 biçiminde sağlamanız gerekir.

      Aşağıdaki adımları hello nasıl toogenerate bir .pfx sertifika dosyası için FairPlay açıklar:

    1. OpenSSL https://slproweb.com/products/Win32OpenSSL.html yükleyin.

        Merhaba FairPlay sertifika ve Apple tarafından sunulan diğer dosyaların nerede toohello klasörüne gidin.
    2. Komut hello komut satırından aşağıdaki hello çalıştırın. Merhaba .cer dosyasını tooa .pem dosyasını dönüştürür.

        "C:\OpenSSL-Win32\bin\openssl.exe" x509-der bildirmek-fairplay.cer içinde-fairplay out.pem çıkışı
    3. Komut hello komut satırından aşağıdaki hello çalıştırın. Bu hello .pem tooa .pfx dosyası hello özel anahtarla dönüştürür. Merhaba .pfx dosyası için Hello parolayı sonra OpenSSL tarafından istendi.

        "C:\OpenSSL-Win32\bin\openssl.exe" pkcs12-- out fairplay out.pfx export-inkey privatekey.pem-fairplay out.pem - passin file:privatekey-pem-pass.txt içinde
  * **Uygulama sertifika parola**: hello .pfx dosyasını oluşturmak için başlangıç parolası.
  * **Uygulama sertifika parolası kimliği**: hello parola, benzer toohow diğer Media Services anahtarları bunlar karşıya yüklemeniz gerekir. Kullanım hello **ContentKeyType.FairPlayPfxPassword** enum değeri tooget hello Media Services kimliği Bu gereksinim duydukları ne olduğunu toouse hello anahtar teslim İlkesi seçeneği içinde.
  * **IV**: 16 bayt rastgele bir değeri budur. Bu eşleşmelidir IV hello varlık teslim İlkesi'nde hello. Oluşturduğunuz IV hello ve her iki yerde de yerleştirin: hello varlık teslim ilkesini ve hello anahtar teslim İlkesi seçeneği.
  * **SORUN**: hello Apple Geliştirici Portalı kullanarak hello sertifika oluşturduğunuzda bu anahtar aldı. Her geliştirme ekibi benzersiz ASK alır. Merhaba ASK bir kopyasını kaydedin ve güvenli bir yerde saklayın. Daha sonra FairPlayAsk tooMedia Hizmetleri olarak tooconfigure ASK ihtiyacınız olacak.
  * **SORUN kimliği**: Media Services'e ASK karşıya yüklediğinizde bu kimliği elde edilir. Hello kullanarak ASK yüklemelisiniz **ContentKeyType.FairPlayAsk** enum değeri. Merhaba sonucunda hello Media Services ID döndürülür ve ne hello anahtar teslim İlkesi seçeneği ayarlarken kullanılması gereken budur.

Merhaba şunları FPS istemci tarafı hello tarafından ayarlanması gerekir:

  * **Uygulama sertifika (AC)**: Bu, bazı yükü hangi hello işletim sisteminin kullandığı tooencrypt hello ortak anahtarı içeren bir.cer/.der dosyasıdır. Merhaba oynatıcısının gerektirdiğinden Media Services tooknow ilgili gerekir. Merhaba anahtar teslim hizmeti hello karşılık gelen özel anahtarı kullanarak şifresini çözer.

tooplay FairPlay şifrelenmiş akış geri, gerçek ASK ilk ulaşmak ve gerçek bir sertifika oluşturur. Bu işlem, tüm üç bölümden oluşturur:

  * .DER dosya
  * .pfx dosyası
  * Merhaba .pfx için parolayı

Merhaba aşağıdaki istemcileri desteklemek ile HLS **AES-128 CBC** şifreleme: OS X, Apple TV iOS Safari.

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a>FairPlay dinamik şifreleme ve lisans teslimat hizmetlerini yapılandırma
Merhaba, FairPlay ile varlıklarınızı hello Media Services lisans teslimat hizmeti kullanarak ve dinamik şifreleme kullanarak koruma için genel adımlar verilmiştir.

1. Bir varlık oluşturun ve dosyaları hello varlığa yükleyin.
2. Merhaba dosya toohello Uyarlamalı bit hızı MP4 kümesine içeren hello varlık kodlayın.
3. Bir içerik anahtarı oluşturup kodlanmış hello varlıkla ilişkilendirin.  
4. Merhaba içerik anahtarının yetkilendirme ilkesini yapılandırın. Merhaba aşağıdakileri belirtin:

   * Merhaba teslim yöntemini (Bu durumda, FairPlay).
   * FairPlay ilkesi seçenekleri yapılandırma. Ayrıntılar için tooconfigure FairPlay, bkz: Merhaba **ConfigureFairPlayPolicyOptions()** aşağıdaki hello örneği yöntemi.

     > [!NOTE]
     > Genellikle, yalnızca bir sertifika ve ASK kümesi olacağı için yalnızca bir kez tooconfigure FairPlay ilkesi seçenekleri istersiniz.
     >
     >
   * Kısıtlamalar (açık veya belirteç).
   * Başlangıç anahtarı toohello istemci nasıl teslim edildiğini tanımlayan bilgileri belirli toohello anahtar teslim türüne.
5. Merhaba varlık teslim ilkesini yapılandırın. Merhaba teslim ilkesi yapılandırması şunları içerir:

   * Merhaba teslim Protokolü (HLS).
   * dinamik şifreleme (ortak CBC şifreleme) Hello türü.
   * Merhaba lisans edinme URL'si.

     > [!NOTE]
     > Toodeliver FairPlay ve başka bir dijital hak yönetimi (DRM) sistemiyle şifrelenmiş bir akış istiyorsanız, tooconfigure ayrı teslim ilkeleri vardır:
     >
     > * Bir IAssetDeliveryPolicy tooconfigure dinamik Uyarlamalı akış HTTP (DASH) ile ortak şifreleme (CENC) (PlayReady + Widevine) ve kesintisiz PlayReady ile üzerinden
     > * Başka bir IAssetDeliveryPolicy tooconfigure FairPlay HLS için
     >
     >
6. Bir OnDemand Bulucu tooget bir akış URL'si oluşturun.

## <a name="use-fairplay-key-delivery-by-player-apps"></a>FairPlay anahtar teslim tarafından oynatıcı uygulamaları kullanma
Merhaba iOS SDK'sını kullanarak oynatıcı uygulamaları geliştirme yapabilirsiniz. toobe mümkün tooplay FairPlay içeriği, tooimplement hello lisans değişimi Protokolü sahip. Bu protokol, Apple tarafından belirtilmemiş. Bu, tooeach uygulamasını nasıl toosend anahtar teslim istekleri olur. Merhaba Media Services FairPlay anahtar teslim hizmeti hello SPC toocome www-form-url kodlanmış post ileti, form aşağıdaki hello olarak bekler:

    spc=<Base64 encoded SPC>

> [!NOTE]
> Azure Media Player hello kutusu dışında FairPlay oynatmayı desteklemiyor. MAC OS X, tooget FairPlay kayıttan yürütme, Apple developer hesabı hello hello örnek oynatıcı edinin.
>
>

## <a name="streaming-urls"></a>Akış URL'leri
Varlığınızı birden çok DRM ile şifrelenmiş bir şifreleme etiketi akış URL'si hello kullanmalısınız: (biçimi 'm3u8-aapl' = şifreleme = 'xxx').

ilgili önemli noktalar aşağıdaki hello Uygula:

* Yalnızca sıfır veya bir şifreleme türü belirtilebilir.
* Merhaba şifreleme türü bir şifreleme uygulanan toohello varlık ise yalnızca hello URL'SİNDE belirtilen toobe sahip değil.
* Merhaba şifreleme türü büyük küçük harfe duyarlı değil.
* şu şifreleme türlerini hello belirtilebilir:  
  * **cenc**: ortak şifreleme (PlayReady veya Widevine)
  * **cbcs-aapl**: FairPlay
  * **CBC**: AES zarfı şifreleme

## <a name="create-and-configure-a-visual-studio-project"></a>Visual Studio projesi oluşturup yapılandırma

1. Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md). 
2. Öğeleri çok aşağıdaki hello eklemek**appSettings** app.config dosyasında tanımlanan:

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a>Örnek

örnek aşağıdaki hello hello özelliği toouse Media Services toodeliver FairPlay ile şifrelenmiş içeriğinizi gösterir. Bu işlevsellik için .NET sürüm 3.6.0 hello Azure Media Services SDK'sı sunulmuştur. 

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
    using Microsoft.WindowsAzure.MediaServices.Client.FairPlay;
    using Newtonsoft.Json;
    using System.Security.Cryptography.X509Certificates;

    namespace DynamicEncryptionWithFairPlay
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

            IContentKey key = CreateCommonCBCTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("FairPlay License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay));
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

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted HLS URL: {0}/manifest(format=m3u8-aapl)", url);

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

            IJob job = _context.Jobs.Create(String.Format("Encoding {0}", inputAsset.Name));

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

        static public IContentKey CreateCommonCBCTypeContentKey(IAsset asset)
        {
            // Create HLS SAMPLE AES encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryptionCbcs);

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


            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();

            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
            ContentKeyDeliveryType.FairPlay,
            restrictions,
            FairPlayConfiguration);


            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with no restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

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

            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();


            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                   ContentKeyDeliveryType.FairPlay,
                   restrictions,
                   FairPlayConfiguration);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with hello cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound tooa real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key toogenerate hello response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating hello .pfx file.
            string pfxPassword = "<customer password for creating hello .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key toogenerate hello response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match hello iv in hello asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify hello .pfx file created by hello customer.
            var appCert = new X509Certificate2("path toohello .pfx file created by hello customer", pfxPassword, X509KeyStorageFlags.Exportable);

            string FairPlayConfiguration =
            Microsoft.WindowsAzure.MediaServices.Client.FairPlay.FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration(
                appCert,
                pfxPassword,
                pfxPasswordId,
                askId,
                iv);

            return FairPlayConfiguration;
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

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            var kdPolicy = _context.ContentKeyAuthorizationPolicies.Where(p => p.Id == key.AuthorizationPolicyId).Single();

            var kdOption = kdPolicy.Options.Single(o => o.KeyDeliveryType == ContentKeyDeliveryType.FairPlay);

            FairPlayConfiguration configFP = JsonConvert.DeserializeObject<FairPlayConfiguration>(kdOption.KeyDeliveryConfiguration);

            // Get hello FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // hello reason hello below code replaces "https://" with "skd://" is because
            // in hello IOS player sample code which you obtained in Apple developer account,
            // hello player only recognizes a Key URL that starts with skd://.
            // However, if you are using a customized player,
            // you can choose whatever protocol you want.
            // For example, "https".

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.FairPlayLicenseAcquisitionUrl, acquisitionUrl.ToString().Replace("https://", "skd://")},
                    {AssetDeliveryPolicyConfigurationKey.CommonEncryptionIVForCbcs, configFP.ContentEncryptionIV}
            };

            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryptionCbcs,
            AssetDeliveryProtocol.HLS,
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


## <a name="next-steps-media-services-learning-paths"></a>Sonraki adımlar: Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
