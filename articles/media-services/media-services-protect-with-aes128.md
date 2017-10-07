---
title: "aaaUsing AES-128 dinamik şifreleme ve anahtar teslim hizmeti | Microsoft Docs"
description: "Microsoft Azure Media Services, toodeliver AES 128 bit şifreleme anahtarları ile şifrelenmiş içeriğinizi sağlar. Media Services de şifreleme anahtarlarını tooauthorized kullanıcılar sunar hello anahtar teslim hizmeti sağlar. Bu konu, nasıl toodynamically AES-128 ile şifrelemek ve hello anahtar teslim Hizmeti'yle gösterir."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 4d2c10af-9ee0-408f-899b-33fa4c1d89b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: cb1b413ec2ba79f7437464099cf72236ab93f312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-aes-128-dynamic-encryption-and-key-delivery-service"></a>AES-128 dinamik şifreleme ve anahtar teslim hizmeti kullanma
> [!div class="op_single_selector"]
> * [.NET](media-services-protect-with-aes128.md)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>Genel Bakış
> [!NOTE]
> Bkz: [bu](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) tooprotect medyanızı AES şifreleme ile nasıl içerik genel bir bakış için video.
> 
> 

Microsoft Azure Media Services toodeliver Http canlı-akış (HLS) ve Gelişmiş Şifreleme Standardı ((128-bit şifreleme anahtarları kullanılarak) AES ile) şifrelenmiş kesintisiz akışlara sağlar. Media Services de şifreleme anahtarlarını tooauthorized kullanıcılar sunar hello anahtar teslim hizmeti sağlar. Bir varlık için Media Services tooencrypt istiyorsanız, tooassociate hello varlık ile bir şifreleme anahtarı gerekir ve ayrıca hello anahtarı için yetkilendirme ilkelerini yapılandırın. Bir akış player tarafından istendiğinde Media Services belirtilen hello kullanan anahtar toodynamically AES şifreleme kullanarak içeriğinizi şifreleyin. toodecrypt hello akış hello anahtar teslim hizmetinden hello anahtar hello player isteyin. tooget hello anahtar desteklemediğini hello kullanıcıdır toodecide yetkili, hello hizmet hello anahtar için belirtilen hello yetkilendirme ilkelerini değerlendirir.

Media Services, anahtar isteğinde bulunan kullanıcıların kimlik doğrulamasını yapmanın birden çok yöntemini destekler. Merhaba içerik anahtarı yetkilendirme ilkesini bir veya daha fazla yetkilendirme kısıtlamaları olabilir: açık veya belirteç kısıtlama. Merhaba belirteç kısıtlamalı ilkenin, bir güvenli belirteç hizmeti (STS) tarafından verilmiş bir belirteç tarafından eklenmelidir. Media Services hello belirteçleri destekler [basit Web belirteçleri](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) biçimi ve [JSON Web belirteci](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) biçimi. Daha fazla bilgi için bkz: [hello içerik anahtarının yetkilendirme ilkesini yapılandırma](media-services-protect-with-aes128.md#configure_key_auth_policy).

tootake avantajı dinamik şifrelenmesi toohave Çoklu bit hızlı MP4 dosyası ya da Çoklu bit hızlı kesintisiz akış kaynak dosyası içeren bir varlık gerekir. Ayrıca (Bu konunun ilerleyen bölümlerinde açıklanan) hello varlık için tooconfigure hello teslim ilkesini gerekir. Ardından, akış URL'si hello belirtilen hello biçime bağlı olarak, hello isteğe bağlı Akış sunucusu bu hello akış seçmiş olduğunuz hello protokolde teslim güvence altına alır. Sonuç olarak, yalnızca toostore gerekir ve tek bir depolama biçiminde ve Media Services hizmeti hello dosyaları ödeme hello istemciden gelen isteklere göre uygun yanıtı derler ve.

Bu konu, korumalı medya teslim eden uygulamalar üzerinde çalışması yararlı toodevelopers olacaktır. Merhaba konu nasıl tooconfigure hello anahtar teslim hizmeti Yetkilendirme İlkeleri ile yalnızca yetkili istemcilerin hello şifreleme anahtarları alabilir böylece gösterir. Ayrıca gösterir nasıl toouse dinamik şifreleme.


## <a name="aes-128-dynamic-encryption-and-key-delivery-service-workflow"></a>AES-128 dinamik şifreleme ve anahtar teslim hizmeti iş akışı

Merhaba, varlıklarınızı hello Media Services anahtar teslimat hizmeti ve dinamik şifreleme kullanarak AES ile şifrelerken tooperform gerekir genel adımlar şunlardır.

1. [Bir varlık oluşturun ve dosyaları hello varlığa yükleyin](media-services-protect-with-aes128.md#create_asset).
2. [Merhaba varlığı içeren Hello dosya toohello bit hızı Uyarlamalı MP4 kümesine kodlayın](media-services-protect-with-aes128.md#encode_asset).
3. [Bir içerik anahtarı oluşturup kodlanmış hello varlıkla ilişkilendirme](media-services-protect-with-aes128.md#create_contentkey). Media Services'de hello içerik anahtarı hello varlığın şifreleme anahtarını içerir.
4. [Merhaba içerik anahtarının yetkilendirme ilkesini yapılandırma](media-services-protect-with-aes128.md#configure_key_auth_policy). Merhaba içerik anahtarı yetkilendirme ilkesinin tarafınızdan yapılandırılması ve hello içerik anahtar toobe teslim toohello istemcisi için sırayla hello istemci tarafından karşılanır.
5. [Bir varlık için Hello teslim ilkesini yapılandırma](media-services-protect-with-aes128.md#configure_asset_delivery_policy). Merhaba teslim ilkesi yapılandırması içerir: anahtar edinme URL'si ve başlatma vektörü (IV) (AES 128 gerektiren aynı IV toobe sağlanan şifrelerken hello ve çözme) teslim Protokolü (örneğin, MPEG DASH, HLS, kesintisiz akış veya tümü), hello türü dinamik şifreleme (örneğin, zarf veya dinamik şifreleme).

    Merhaba üzerinde farklı ilke tooeach Protokolü uygulayabilir aynı varlık. Örneğin, PlayReady şifreleme tooSmooth/DASH ve AES zarfı tooHLS uygulayabilirsiniz. Bir teslim ilkesinde tanımlanmayan tüm protokollerin (örneğin, yalnızca hello protokol olarak HLS belirten tek bir ilke ekliyorsunuz) akışla aktarılması engellenir. Merhaba özel durum toothis hiç tanımlanmış hiçbir varlık teslim ilkesini varsa ' dir. Ardından, tüm protokoller hello Temizle izin verilir.

6. [Bir OnDemand Bulucu oluşturmanız](media-services-protect-with-aes128.md#create_locator) içinde bir akış URL'si tooget sipariş.

Merhaba konu aynı zamanda gösterir [bir istemci uygulaması hello anahtar teslim hizmetinden bir anahtar nasıl isteyebilir](media-services-protect-with-aes128.md#client_request).

Tam .NET bulacaksınız [örnek](media-services-protect-with-aes128.md#example) hello konu hello sonunda.

Görüntü aşağıdaki hello yukarıda açıklanan hello akışı gösterilmektedir. Burada hello belirteci kimlik doğrulaması için kullanılır.

![AES-128 ile koruma](./media/media-services-content-protection-overview/media-services-content-protection-with-aes.png)

Bu konunun geri kalanında Hello ayrıntılı açıklamalar, kod örnekleri ve nasıl tooachieve hello yukarıda açıklanan görevleri göster bağlantılar tootopics sağlar.

## <a name="current-limitations"></a>Geçerli sınırlamalar
Varlığınızın teslim ilkesini ekler veya güncelleştirirseniz, mevcut bulucuyu (varsa) silip yeni bir bulucu oluşturmanız gerekir.

## <a id="create_asset"></a>Bir varlık oluşturun ve dosyaları hello varlığa yükleyin
Sipariş toomanage kodlamak ve videolarınızı, akış içeriğinizi önce Microsoft Azure Media Services'e yüklemeniz gerekir. Yüklenmesinin ardından içeriğiniz daha fazla işleme ve akış hello bulutta güvenli bir şekilde depolanır. 

Ayrıntılı bilgi için bkz. [Media Services hesabına dosya yükleme](media-services-dotnet-upload-files.md).

## <a id="encode_asset"></a>Merhaba varlık içeren hello dosya toohello Uyarlamalı bit hızı MP4 kümesine kodlayın
Dinamik şifreleme ile tek ihtiyacınız olan toocreate Çoklu bit hızlı MP4 dosyası ya da Çoklu bit hızlı kesintisiz akış kaynak dosyası içeren bir varlık. Merhaba hello bildiriminde belirtilen biçime bağlı olarak veya istek parçalara, hello isteğe bağlı Akış sunucusu, hello akış seçmiş olduğunuz hello protokolde almanızı sağlar. Sonuç olarak, yalnızca toostore gerekir ve tek bir depolama biçiminde ve Media Services hizmeti hello dosyaları ödeme hello istemciden gelen isteklere göre uygun yanıtı derler ve. Daha fazla bilgi için bkz: Merhaba [dinamik paketlemeye genel bakış](media-services-dynamic-packaging-overview.md) konu.

>[!NOTE]
>AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu. İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu. 
>
>Ayrıca, toobe mümkün toouse dinamik paketleme ve dinamik şifreleme Varlığınızı içermelidir Uyarlamalı bit hızlı MP4s veya uyarlamalı bit hızlı kesintisiz akış dosyaları kümesidir.

Yönergeler için tooencode, bkz: [nasıl tooencode medya Kodlayıcı standart kullanarak bir varlık](media-services-dotnet-encode-with-media-encoder-standard.md).

## <a id="create_contentkey"></a>Bir içerik anahtarı oluşturup kodlanmış hello varlıkla ilişkilendirme
Media Services'de hello içerik anahtarı tooencrypt bir varlık istediğiniz başlangıç anahtarı içeren ile.

Ayrıntılı bilgi için bkz. [İçerik anahtarı oluşturma](media-services-dotnet-create-contentkey.md).

## <a id="configure_key_auth_policy"></a>Merhaba içerik anahtarının yetkilendirme ilkesini yapılandırın
Media Services, anahtar isteğinde bulunan kullanıcıların kimlik doğrulamasını yapmanın birden çok yöntemini destekler. Merhaba içerik anahtarı yetkilendirme ilkesinin tarafınızdan yapılandırılması ve hello anahtar toobe toohello istemci teslim sırayla hello istemci (oynatıcı) tarafından karşılanır. Merhaba içerik anahtarı yetkilendirme ilkesini bir veya daha fazla yetkilendirme kısıtlamaları olabilir: açın, simge restriction ya da IP kısıtlaması.

Ayrıntılı bilgi için bkz. [İçerik Anahtarı Yetkilendirme İlkesini Yapılandırma](media-services-dotnet-configure-content-key-auth-policy.md).

## <a id="configure_asset_delivery_policy"></a>Varlık teslim ilkesini yapılandırma
Varlığınıza Hello teslim ilkesini yapılandırın. Varlık teslim ilkesi yapılandırması hello bazı şeyleri içerir:

* başlangıç anahtarı edinme URL'si. 
* Merhaba başlatma vektörü (IV) toouse hello Zarf şifreleme için. AES 128, şifreleme ve şifre çözme aynı IV toobe sağlanan hello gerektirir. 
* Merhaba varlık teslim Protokolü (örneğin, MPEG DASH, HLS, kesintisiz akış veya tümü).
* dinamik şifreleme (örneğin, AES zarfı) Hello türü veya dinamik şifreleme yok. 

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

## <a id="client_request"></a>Nasıl istemciniz bir anahtar hello anahtar teslim hizmetinden isteyebilir miyim?
Merhaba önceki adımda tooa bildirim dosyası işaret eden hello URL oluşturulur. İstemci tooextract hello gerekli bilgileri sipariş toomake isteği toohello anahtar teslim hizmeti bildirim dosyalarından akış hello gerekir.

### <a name="manifest-files"></a>Bildirim dosyası
Merhaba istemci gerekir (aynı zamanda içerik anahtarı kimliği (çocuk) içeren) tooextract hello URL hello bildirim dosyası değeri. Merhaba istemci tooget hello şifreleme anahtarı hello anahtar teslim hizmetinden daha sonra deneyecek. Merhaba istemcisini de tooextract hello IV değeri gerekiyor ve aşağıdaki kod parçacığında hello stream.hello şifresini kullanım gösterir hello <Protection> hello kesintisiz akış bildiriminin öğesi.

    <Protection>
      <ProtectionHeader SystemID="B47B251A-2409-4B42-958E-08DBAE7B4EE9">
        <ContentProtection xmlns:sea="urn:mpeg:dash:schema:sea:2012" schemeIdUri="urn:mpeg:dash:sea:2012">
          <sea:SegmentEncryption schemeIdUri="urn:mpeg:dash:sea:aes128-cbc:2013"/>
          <sea:KeySystem keySystemUri="urn:mpeg:dash:sea:keysys:http:2013"/>
          <sea:CryptoPeriod IV="0xD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7" 
                            keyUriTemplate="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
                                            kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d"/>
        </ContentProtection>
      </ProtectionHeader>
    </Protection>

HLS Hello durumda hello kök bildirimi segment dosyalarıyla ayrılır. 

Örneğin, hello kök bildirimidir: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) ve segment dosya adlarının bir listesini içerir.

    . . . 
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=630133,RESOLUTION=424x240,CODECS="avc1.4d4015,mp4a.40.2",AUDIO="audio"
    QualityLevels(514369)/Manifest(video,format=m3u8-aapl)
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=965441,RESOLUTION=636x356,CODECS="avc1.4d401e,mp4a.40.2",AUDIO="audio"
    QualityLevels(842459)/Manifest(video,format=m3u8-aapl)
    …

Merhaba segment dosyalardan birini (örneğin, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should metin düzenleyicide açın #EXT-X-hello dosyayı şifreli gösteren anahtar içerir.

    #EXTM3U
    #EXT-X-VERSION:4
    #EXT-X-ALLOW-CACHE:NO
    #EXT-X-MEDIA-SEQUENCE:0
    #EXT-X-TARGETDURATION:9
    #EXT-X-KEY:METHOD=AES-128,
    URI="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
         kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d",
            IV=0XD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7
    #EXT-X-PROGRAM-DATE-TIME:1970-01-01T00:00:00.000+00:00
    #EXTINF:8.425708,no-desc
    Fragments(video=0,format=m3u8-aapl)
    #EXT-X-ENDLIST

>[!NOTE] 
>Tooplay planlıyorsanız bir AES HLS Safari'de şifrelenmiş bkz [bu blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).

### <a name="request-hello-key-from-hello-key-delivery-service"></a>Merhaba anahtar teslim hizmetinden Hello anahtarı iste

Merhaba aşağıdaki kod nasıl toosend isteği toohello Media Services anahtar teslim hizmeti anahtar teslim (Merhaba bildirimden ayıklandı) URI kullanılarak gösterir ve bir belirteç (Bu konuda değil konuşun nasıl tooget basit Web güvenli bir belirteci Hizmeti'nden belirteçleri hakkında).

    private byte[] GetDeliveryKey(Uri keyDeliveryUri, string token)
    {
        HttpWebRequest request = (HttpWebRequest)WebRequest.Create(keyDeliveryUri);

        request.Method = "POST";
        request.ContentType = "text/xml";
        if (!string.IsNullOrEmpty(token))
        {
            request.Headers[AuthorizationHeader] = token;
        }
        request.ContentLength = 0;

        var response = request.GetResponse();

        var stream = response.GetResponseStream();
        if (stream == null)
        {
            throw new NullReferenceException("Response stream is null");
        }

        var buffer = new byte[256];
        var length = 0;
        while (stream.CanRead && length <= buffer.Length)
        {
            var nexByte = stream.ReadByte();
            if (nexByte == -1)
            {
                break;
            }
            buffer[length] = (byte)nexByte;
            length++;
        }
        response.Close();

        // AES keys must be exactly 16 bytes (128 bits).
        var key = new byte[length];
        Array.Copy(buffer, key, length);
        return key;
    }

## <a name="protect-your-content-with-aes-128-using-net"></a>İçeriğinizi AES-128 ile korumak .NET kullanma

### <a name="create-and-configure-a-visual-studio-project"></a>Visual Studio projesi oluşturup yapılandırma

1. Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md). 
2. Öğeleri çok aşağıdaki hello eklemek**appSettings** app.config dosyasında tanımlanan:

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

### <a id="example"></a>Örnek

Bu bölümde gösterilen hello koduyla Hello kodu Program.cs dosyanızdaki üzerine.
 
>[!NOTE]
>Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için). Merhaba kullanması gereken her zaman kullanıyorsanız, aynı ilke kimliği hello aynı gün / erişim izinlerini, örneğin, uzun bir süre (karşıya yükleme olmayan ilkeleri) yerinde hedeflenen tooremain olan bulucular ilkeleri. Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.

Emin tooupdate değişkenleri, giriş dosyalarınızın bulunduğu toopoint toofolders olun.

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Security.Cryptography;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace AESDynamicEncryptionAndKeyDeliverySvc
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // A Uri describing hello issuer of hello token.  
        // Must match hello value in hello token for hello token toobe considered valid.
        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        // hello Audience or Scope of hello token.  
        // Must match hello value in hello token for hello token toobe considered valid.
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

            IContentKey key = CreateEnvelopeTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified 
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

            //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
            //so you have tooadd it in front of hello token string. 
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello bit.ly/aesplayer Flash player tootest hello URL 
            // (with open authorization policy). 
            // Paste hello URL and click hello Update button tooplay hello video. 
            //
            string URL = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Smooth Streaming Url: {0}/manifest", URL);
            Console.WriteLine();
            Console.WriteLine("HLS Url: {0}/manifest(format=m3u8-aapl)", URL);
            Console.WriteLine();

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
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.StorageEncrypted);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);


            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with hello encoding details, using a string preset.
            // In this case "Adaptive Streaming" preset is used.
            ITask task = job.Tasks.AddNew("My encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
            ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }

        static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
        {
            // Create envelope encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                keyId,
                contentKey,
                "ContentKey",
                ContentKeyType.EnvelopeEncryption);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }

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

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);

            string envelopeEncryptionIV = Convert.ToBase64String(GetRandomBuffer(16));

            // When configuring delivery policy, you can choose tooassociate it
            // with a key acquisition URL that has a KID appended or
            // or a key acquisition URL that does not have a KID appended  
            // in which case a content key can be reused. 

            // EnvelopeKeyAcquisitionUrl:  contains a key ID in hello key URL.
            // EnvelopeBaseKeyAcquisitionUrl:  hello URL does not contains a key ID

            // hello following policy configuration specifies: 
            // key url that will have KID=<Guid> appended toohello envelope and
            // hello Initialization Vector (IV) toouse for hello envelope encryption.

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeKeyAcquisitionUrl, keyAcquisitionUri.ToString()}
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
            Console.WriteLine("Adding Asset Delivery Policy: " +
            assetDeliveryPolicy.AssetDeliveryPolicyType);
        }

        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset. 

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                EndsWith(".ism")).
                FirstOrDefault();

            // Create a 30-day readonly access policy. 
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
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

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int size)
        {
            byte[] randomBytes = new byte[size];
            using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
            {
            rng.GetBytes(randomBytes);
            }

            return randomBytes;
        }
        }
    }


## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

