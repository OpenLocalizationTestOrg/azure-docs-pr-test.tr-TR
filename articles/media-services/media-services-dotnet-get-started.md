---
title: "aaaGet başlatılan .NET kullanarak isteğe bağlı içerik göndermeye | Microsoft Docs"
description: "Bu öğreticide hello .NET kullanarak Azure Media Services ile bir üzerinde isteğe bağlı içerik teslim uygulaması gerçekleştirilmesinin adımları açıklanmaktadır."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 388b8928-9aa9-46b1-b60a-a918da75bd7b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 4ca9394bd581e1d9062e5a008a410b2c058e017e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a>.NET SDK kullanarak isteğe bağlı içerik göndermeye başlama
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

Bu öğreticide, hello Azure Media Services .NET SDK kullanarak Azure Media Services (AMS) uygulaması ile temel bir isteğe bağlı video (VoD) içerik teslim hizmeti uygulamanın hello adımları açıklanmaktadır.

## <a name="prerequisites"></a>Ön koşullar

Merhaba, gerekli toocomplete hello öğretici şunlardır:

* Bir Azure hesabı. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).
* Bir Media Services hesabı. bir Media Services hesabı toocreate bkz [nasıl tooCreate Media Services hesabı](media-services-portal-create-account.md).
* .NET framework 4.0 veya sonraki sürümü.
* Visual Studio.

Bu öğretici hello aşağıdaki görevleri içerir:

1. Akış uç noktası (hello Azure portal kullanarak) başlatın.
2. Visual Studio projesi oluşturun ve yapılandırın.
3. Toohello Media Services hesabına bağlanın.
2. Bir video dosyası yükleyin.
3. Merhaba kaynak dosya bit hızı Uyarlamalı MP4 dosyaları kümesine kodlayın.
4. Merhaba varlık ve get akış ve aşamalı indirme URL'leri yayımlayın.  
5. İçeriğinizi oynatın.

## <a name="overview"></a>Genel Bakış
Bu öğreticide hello .NET için Azure Media Services (AMS) SDK kullanarak isteğe bağlı video (VoD) içerik teslim uygulaması gerçekleştirilmesinin adımları açıklanmaktadır.

Başlangıç Öğreticisi hello temel Media Services iş akışı, hello en genel programlama nesnelerini ve Media Services geliştirmek için gereken görevleri tanıtır. Başlangıç Öğreticisi Hello tamamlandığında mümkün toostream olması veya aşamalı olarak örnek bir medya dosyasını karşıya kodlanmış ve yüklenen indirebilirsiniz.

### <a name="ams-model"></a>AMS modeli

Merhaba aşağıdaki görüntüde bazılarını hello en yaygın olarak kullanılan nesneler hello Media Services OData modelde VoD uygulamaları geliştirirken gösterir.

Merhaba görüntü tooview boyutu tam'ı tıklatın.  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

Merhaba tüm model görüntüleyebilirsiniz [burada](https://media.windows.net/API/$metadata?api-version=2.15).  

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a>Akış uç noktaları Hello Azure portal kullanarak Başlat

Merhaba en sık karşılaşılan senaryolardan biri, video bit hızı Uyarlamalı akış iletmektir Azure Media Services ile çalışırken. Media Services, bit hızı Uyarlamalı MP4 kodlanmış içeriğinizi Media Services (MPEG DASH, HLS, kesintisiz akış) tam zamanında tarafından önceden paketlenmiş toostore kalmadan desteklenen akış biçimlerinde toodeliver sağlayan dinamik paketleme sağlar Bu akış biçimlerine her da sürümleri.

>[!NOTE]
>AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu. İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu.

toostart akış uç Merhaba, aşağıdaki hello:

1. Merhaba oturum açma [Azure portal](https://portal.azure.com/).
2. Hello Ayarları penceresinde, akış uç noktaları'ı tıklatın.
3. Merhaba varsayılan akış uç noktası'ı tıklatın.

    Merhaba varsayılan akış uç noktası AYRINTILAR penceresi görüntülenir.

4. Merhaba başlangıç simgesine tıklayın.
5. Merhaba Kaydet düğmesine toosave değişikliklerinizi'ı tıklatın.

## <a name="create-and-configure-a-visual-studio-project"></a>Visual Studio projesi oluşturup yapılandırma

1. Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md). 
2. Yeni bir klasör oluşturun (klasör herhangi bir yerde olabilir yerel diskinize) ve tooencode ve akış istediğiniz veya aşamalı indirmek bir .mp4 dosyasını kopyalayın. Bu örnekte "C:\VideoFiles" yolu hello kullanılır.

## <a name="connect-toohello-media-services-account"></a>Toohello Media Services hesabına bağlanma

Media Services .NET ile kullanırken hello kullanmalısınız **CloudMediaContext** çoğu Media Services programlama görevlerinin sınıfı: tooMedia Services hesabına bağlanma; oluşturma, güncelleştirme, erişme ve hello aşağıdaki silme nesneleri: varlıklar, varlık dosyaları, işler, erişim ilkeleri, bulucular vb..

Koddan hello ile Merhaba varsayılan Program sınıfının üzerine. Merhaba kod tooread hello bağlantı hello App.config dosyasından değerleri nasıl ve ne göstermektedir toocreate hello **CloudMediaContext** sipariş tooconnect tooMedia nesnesinde Hizmetleri. Daha fazla bilgi için bkz: [toohello Media Services API bağlanma](media-services-use-aad-auth-to-access-ams-api.md).

Sahip olduğunuz emin tooupdate hello dosya adı ve yolu toowhere medya dosyanızın olun.

Merhaba **ana** işlevi açıklanacak olan yöntemleri çağırır bu bölümün sonraki kısımlarında.

> [!NOTE]
> Tanımları tüm hello işlevler için eklenene kadar derleme hataları alma.

    class Program
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
        try
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Add calls toomethods defined in this section.
            // Make sure tooupdate hello file name and path toowhere you have your media file.
            IAsset inputAsset =
            UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.None);

            IAsset encodedAsset =
            EncodeToAdaptiveBitrateMP4s(inputAsset, AssetCreationOptions.None);

            PublishAssetGetURLs(encodedAsset);
        }
        catch (Exception exception)
        {
            // Parse hello XML error message in hello Media Services response and create a new
            // exception with its content.
            exception = MediaServicesExceptionParser.Parse(exception);

            Console.Error.WriteLine(exception.Message);
        }
        finally
        {
            Console.ReadLine();
        }
        }
    }

## <a name="create-a-new-asset-and-upload-a-video-file"></a>Yeni varlık oluşturma ve video dosyası yükleme

Media Services’de, dijital dosyalar bir varlığa yüklenir (veya alınır). Merhaba **varlık** varlık içerebilir video, ses, görüntüler, küçük resim koleksiyonları, metin parçaları ve kapalı açıklamalı alt yazı dosyaları (ve hello meta verileri bu dosyalar hakkında.)  Hello dosyalar yüklendiğinde, içeriğiniz sonraki işleme ve akışla için hello bulutta güvenli bir şekilde depolanır. Merhaba varlık Hello dosyalarında çağrılır **varlık dosyaları**.

Merhaba **UploadFile** çağrıları tanımlanan yöntemi **CreateFromFile** (.NET SDK uzantılarında tanımlanmıştır). **CreateFromFile** hangi hello belirtilen kaynak dosyasının yüklendiği yeni bir varlık oluşturur.

Merhaba **CreateFromFile** yöntemi alır **AssetCreationOptions** olanak sağlayan, hello aşağıdaki varlık oluşturma seçeneklerden birini belirtin:

* **Hiçbiri**: Şifreleme kullanılmaz. Merhaba varsayılan değer budur. Bu seçeneği kullandığınızda, içeriğinizin aktarım sırasında ve depolama alanında beklerken korunmadığını unutmayın.
  Aşamalı indirme kullanarak toodeliver bir MP4 planlıyorsanız, bu seçeneği kullanın.
* **StorageEncrypted** -bu seçenek tooencrypt Temizle içeriğinizi tooAzure depolanır depolama şifrelenen yükler Gelişmiş Şifreleme Standardı (AES)-256 bit şifreleme kullanarak yerel olarak kullanın. Depolama şifrelemesi ile korunan varlıklar otomatik olarak şifrelenmemiş ve bir şifrelenmiş dosya sistemi önceki tooencoding ve yeni bir çıkış varlığı olarak geri isteğe bağlı olarak yeniden şifrelenmiş önceki toouploading yerleştirilir. Depolama şifrelemesinin birincil kullanım durumu hello yüksek kaliteli giriş medya dosyalarınızı REST güçlü şifrelemeyle diskte toosecure istediğiniz durumdur.
* **CommonEncryptionProtected**: Zaten Ortak Şifreleme veya PlayReady DRM ile şifrelenip korunan bir içerik (örneğin, PlayReady DRM ile korunan Kesintisiz Akış) yüklüyorsanız bu seçeneği kullanın.
* **EnvelopeEncryptionProtected**: AES ile şifrelenmiş HLS yüklüyorsanız bu seçeneği kullanın. Hello dosyaları gerekir alınan kodlanmış ve Transform Manager tarafından şifrelenmiş olduğunu unutmayın.

Merhaba **CreateFromFile** yöntemi de bir geri çağırma sırası tooreport hello karşıya yükleme sürüyor hello dosyasının belirtmenizi sağlar.

Aşağıdaki örneğine hello belirttiğimiz **hiçbiri** hello varlık seçenekleri için.

Yöntem toohello Program sınıfına aşağıdaki hello ekleyin.

    static public IAsset UploadFile(string fileName, AssetCreationOptions options)
    {
        IAsset inputAsset = _context.Assets.CreateFromFile(
            fileName,
            options,
            (af, p) =>
            {
                Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Asset {0} created.", inputAsset.Id);

        return inputAsset;
    }


## <a name="encode-hello-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a>Merhaba kaynak dosya bit hızı Uyarlamalı MP4 dosyaları kümesine kodlayın
Varlıklar Media Services'e alındıktan sonra medya olabilir kodlanmış biçimini, filigran vb. tooclients teslim edilmeden önce. Bu etkinlikler zamanlanmış ve birden fazla arka plan rol örnekleri tooensure yüksek performans ve kullanılabilirlik karşı çalıştırın. Bu etkinliklere işler adı verilir ve her bir iş hello varlık dosyası üzerinde asıl işi hello atomik görevlerin oluşur.

Azure Media Services ile çalışırken, daha önce belirtildiği gibi hello en sık karşılaşılan senaryolardan biri, bit hızı Uyarlamalı tooyour istemcileri akış iletmektir. Media Services dinamik olarak paketini bit hızı Uyarlamalı MP4 dosyaları kümesini biçimleri aşağıdaki hello birine: HTTP canlı akışı (HLS), kesintisiz akış ve MPEG DASH.

tootake avantajı dinamik paketleme, tooencode veya kodlamasını Ara (kaynak) dosyanızı Uyarlamalı bit hızlı MP4 veya uyarlamalı bit hızlı kesintisiz akış dosyaları kümesine ihtiyacınız.  

koddan hello nasıl toosubmit bir kodlama işi gösterir. Merhaba iş tootranscode hello Ara dosyayı Uyarlamalı bit hızlı MP4s kullanarak kümesi belirten bir görev içerir **Medya Kodlayıcısı standart**. tamamlanana kadar hello kod hello iş ve bekler gönderir.

Merhaba işi tamamlandığında, mümkün toostream varlığınız olması veya kodlama dönüştürmenin sonucu olarak oluşturulan MP4 dosyalarını aşamalı indirmek.

Yöntem toohello Program sınıfına aşağıdaki hello ekleyin.

    static public IAsset EncodeToAdaptiveBitrateMP4s(IAsset asset, AssetCreationOptions options)
    {

        // Prepare a job with a single task tootranscode hello specified asset
        // into a multi-bitrate asset.

        IJob job = _context.Jobs.CreateWithSingleTask(
            "Media Encoder Standard",
            "Adaptive Streaming",
            asset,
            "Adaptive Bitrate MP4",
            options);

        Console.WriteLine("Submitting transcoding job...");


        // Submit hello job and wait until it is completed.
        job.Submit();

        job = job.StartExecutionProgressTask(
            j =>
            {
                Console.WriteLine("Job state: {0}", j.State);
                Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
            },
            CancellationToken.None).Result;

        Console.WriteLine("Transcoding job finished.");

        IAsset outputAsset = job.OutputMediaAssets[0];

        return outputAsset;
    }

## <a name="publish-hello-asset-and-get-urls-for-streaming-and-progressive-download"></a>Merhaba varlığı yayımlayın, akış ve aşamalı indirme URL'lerini alın

toostream veya indirme bir varlık, ilk çok "bir Bulucu oluşturarak yayımlamadan". Bulucular hello varlıkta bulunan erişim toofiles sağlar. Media Services iki tür Bulucuyu destekler: OnDemandOrigin bulucuları, kullanılan toostream medya (örneğin, MPEG DASH, HLS veya kesintisiz akış) ve erişim imzası (SAS) bulucular kullanılan toodownload medya dosyaları (SAS bulucular bakın hakkındadahafazlabilgi[bu](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).

### <a name="some-details-about-url-formats"></a>URL biçimleri hakkında bazı ayrıntılar

Merhaba bulucuları oluşturduktan sonra kullanılan toostream olması veya dosyalarınızı karşıdan hello URL'leri oluşturabilirsiniz. Bu öğreticide Hello örnek uygun tarayıcılarda yapıştırabilirsiniz URL'leri çıkarır. Bu bölümde yalnızca farklı biçimlerin neye benzediğini gösteren kısa örnekler verilir.

#### <a name="a-streaming-url-for-mpeg-dash-has-hello-following-format"></a>MPEG DASH bir akış URL'si biçimi aşağıdaki hello sahiptir:

{akış uç noktası adı-media services hesabı adı}.streaming.mediaservices.windows.net/{konum kimliği}/{dosya adı}.ism/Manifest**(format=mpd-time-csf)**

#### <a name="a-streaming-url-for-hls-has-hello-following-format"></a>HLS akış URL'sini biçimini izleyen hello sahiptir:

{akış uç noktası adı-media services hesabı adı}.streaming.mediaservices.windows.net/{konum kimliği}/{dosya adı}.ism/Manifest**(format=m3u8-aapl)**

#### <a name="a-streaming-url-for-smooth-streaming-has-hello-following-format"></a>Bir akış URL'si kesintisiz akış biçimini izleyen hello sahiptir:

{akış uç noktası adı-media services hesabı adı}.streaming.mediaservices.windows.net/{konum kimliği}/{dosya adı}.ism/Manifest


#### <a name="a-sas-url-used-toodownload-files-has-hello-following-format"></a>Bir SAS kullanılan URL toodownload dosyaları biçimini izleyen hello sahiptir:

{blob kapsayıcısı adı}/{varlık adı}/{dosya adı}/{SAS imzası}

Media Services .NET SDK uzantıları, yayımlanmış varlık dönüş URL'leri Merhaba biçimlendirilmiş kullanışlı yardımcı yöntemler sağlar.

Merhaba aşağıdaki kodu kullanan .NET SDK uzantıları toocreate bulucular ve tooget akış ve aşamalı indirme URL'lerini. Merhaba kod ayrıca nasıl toodownload dosyaları tooa yerel klasörü gösterir.

Yöntem toohello Program sınıfına aşağıdaki hello ekleyin.

    static public void PublishAssetGetURLs(IAsset asset)
    {
        // Publish hello output asset by creating an Origin locator for adaptive streaming,
        // and a SAS locator for progressive download.

        _context.Locators.Create(
            LocatorType.OnDemandOrigin,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));

        _context.Locators.Create(
            LocatorType.Sas,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));


        IEnumerable<IAssetFile> mp4AssetFiles = asset
                .AssetFiles
                .ToList()
                .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Get hello Smooth Streaming, HLS and MPEG-DASH URLs for adaptive streaming,
        // and hello Progressive Download URL.
        Uri smoothStreamingUri = asset.GetSmoothStreamingUri();
        Uri hlsUri = asset.GetHlsUri();
        Uri mpegDashUri = asset.GetMpegDashUri();

        // Get hello URls for progressive download for each MP4 file that was generated as a result
        // of encoding.
        List<Uri> mp4ProgressiveDownloadUris = mp4AssetFiles.Select(af => af.GetSasUri()).ToList();


        // Display  hello streaming URLs.
        Console.WriteLine("Use hello following URLs for adaptive streaming: ");
        Console.WriteLine(smoothStreamingUri);
        Console.WriteLine(hlsUri);
        Console.WriteLine(mpegDashUri);
        Console.WriteLine();

        // Display hello URLs for progressive download.
        Console.WriteLine("Use hello following URLs for progressive download.");
        mp4ProgressiveDownloadUris.ForEach(uri => Console.WriteLine(uri + "\n"));
        Console.WriteLine();

        // Download hello output asset tooa local folder.
        string outputFolder = "job-output";
        if (!Directory.Exists(outputFolder))
        {
            Directory.CreateDirectory(outputFolder);
        }

        Console.WriteLine();
        Console.WriteLine("Downloading output asset files tooa local folder...");
        asset.DownloadToFolder(
            outputFolder,
            (af, p) =>
            {
                Console.WriteLine("Downloading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Output asset files available at '{0}'.", Path.GetFullPath(outputFolder));
    }

## <a name="test-by-playing-your-content"></a>İçeriğiniz oynatarak test etme

Merhaba önceki bölümde tanımlanan hello programı çalıştırdığınızda benzer toohello aşağıdaki hello konsol penceresinde görüntülenir URL'leri hello.

Uyarlamalı akış URL'leri:

Kesintisiz Akış

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

HLS

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

MPEG DASH

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

Aşamalı indirme URL'leri (ses ve video).

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


toostream videonuz URL'nizi hello URL'si metin kutusuna hello yapıştırın [Azure Media Services Oynatıcısı](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

tootest aşamalı indirmek için bir URL (örneğin, Internet Explorer, Chrome veya Safari) bir tarayıcıya yapıştırın.

Daha fazla bilgi için aşağıdaki konularda hello bakın:

- [İçeriğinizi mevcut oynatıcılarda oynatma](media-services-playback-content-with-existing-players.md)
- [Video oynatıcı uygulamaları geliştirme](media-services-develop-video-players.md)
- [DASH.js ile bir MPEG-DASH Uyarlamalı Akış Videosunu bir HTML5 Uygulamasına ekleme](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a>Örnek indirme
Merhaba aşağıdaki kod örneği, bu öğreticide oluşturduğunuz hello kodunu içerir: [örnek](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).

## <a name="next-steps"></a>Sonraki Adımlar

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/
