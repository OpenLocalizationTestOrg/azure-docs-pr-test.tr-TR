---
title: "aaaHow tooperform Azure Media Services toocreate Çoklu bit hızı akışları .NET ile birlikte kullanarak canlı akış gerçekleştirme | Microsoft Docs"
description: "Bir kanal oluşturulması hello adımlarında size tek bit hızında bir canlı akışı alıp .NET SDK kullanarak toomulti bit hızında akışa kodlayan Bu öğretici yetenekte."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 4df5e690-ff63-47cc-879b-9c57cb8ec240
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 22088e6a78a49bd839575614a7c17a411ae8081c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams-with-net"></a>.NET ile Azure Media Services toocreate Çoklu bit hızlı kullanarak tooperform canlı akış nasıl akışları
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [.NET](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [REST API](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> [!NOTE]
> toocomplete Bu öğretici bir Azure hesabınızın olması gerekir. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
> 
> 

## <a name="overview"></a>Genel Bakış
Bu öğretici, oluşturma hello adımlarda size bir **kanal** , tek bit hızında bir canlı akışı alıp toomulti bit hızında akışa kodlayan.

Daha fazla kavramsal bilgi için bkz: Gerçek zamanlı kodlama için etkinleştirilmiş ilgili tooChannels [toocreate Çoklu bit hızı akışları Azure Media Services kullanarak canlı akış](media-services-manage-live-encoder-enabled-channels.md).

## <a name="common-live-streaming-scenario"></a>Ortak Canlı Akış Senaryosu
Aşağıdaki adımları hello ortak canlı akış uygulamaları oluşturmaya dahil olan görevleri açıklar.

> [!NOTE]
> Şu anda hello en fazla canlı bir olay süresi önerilen 8 saattir. Uzun süreyle toorun bir kanal gerekiyorsa lütfen amslived@Microsoft.com adresine başvurun.
> 
> 

1. Bir video kamera tooa bilgisayara bağlayın. Başlatma ve protokolleri aşağıdaki hello birinde tek bit hızlı akış çıkışı sağlayabilecek bir şirket içi gerçek zamanlı Kodlayıcı yapılandırın: RTMP, kesintisiz akış veya RTP (MPEG-TS). Daha fazla bilgi için bkz. [Azure Media Services RTMP Desteği ve Gerçek Zamanlı Kodlayıcılar](http://go.microsoft.com/fwlink/?LinkId=532824).

    Bu adım, Kanalınızı oluşturduktan sonra da gerçekleştirilebilir.

2. Bir Kanal oluşturup başlatın.
3. Alma hello kanal URL'sini alma.

    Merhaba alma URL hello gerçek zamanlı Kodlayıcı toosend hello akış toohello kanal tarafından kullanılır.

4. Merhaba kanal Önizleme URL'sini alın.

    Kanalınızı hello Canlı akışı düzgün şekilde aldığını bu URL tooverify kullanın.

5. Bir varlık oluşturun.
6. Kayıttan yürütme sırasında dinamik olarak şifrelenmiş hello varlık toobe isterseniz, aşağıdaki hello:
7. Bir içerik anahtarı oluşturun.
8. Merhaba içerik anahtarının yetkilendirme ilkesini yapılandırın.
9. Varlık teslim ilkesini (dinamik paketleme ve dinamik şifreleme tarafından kullanılır) yapılandırın.
10. Bir program oluşturun ve oluşturduğunuz toouse hello varlık belirtin.
11. Bir OnDemand Bulucu oluşturarak Hello programla ilişkili hello varlığı yayımlayın.

    >[!NOTE]
    >AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu. Akış uç noktası toostream içerik istediğiniz hello sahip toobe hello **çalıştıran** durumu. 

12. Akışı ve arşivlemeyi hazır toostart olduğunda hello programını başlatın.
13. İsteğe bağlı olarak, gerçek zamanlı Kodlayıcı hello iş toostart bir tanıtım olabilir. Merhaba tanıtım hello çıktı akışına eklenir.
14. Toostop akış ve arşivleme hello olayı istediğinizde hello programı durdurun.
15. Merhaba programı silin (ve isteğe bağlı olarak hello varlığını silme).

## <a name="what-youll-learn"></a>Öğrenecekleriniz
Bu konu, nasıl gösterir tooexecute farklı işlemler Kanallar ve Media Services .NET SDK kullanarak programları. İşlemlerin çoğu uzun süre çalışacağından, uzun süre çalışan işlemleri yöneten .NET API'leri kullanılmaktadır.

Merhaba konu gösterir nasıl toodo hello aşağıdaki:

1. Bir kanal oluşturup başlatın. Uzun süre çalışan API'ler kullanılacaktır.
2. Alma hello kanalları alma (giriş) uç noktası. Bu uç noktaya, tek bit hızlı canlı akış gönderebilen toohello Kodlayıcı sağlanmalıdır.
3. Merhaba Önizleme uç noktasını alın. Bu uç noktaya kullanılan toopreview, akışıdır.
4. İçeriğinizi kullanılan toostore olacak bir varlık oluşturun. Merhaba varlık teslim ilkeleri de, bu örnekte gösterildiği gibi yapılandırılması gerekir.
5. Bir program oluşturun ve daha önce oluşturulan toouse hello varlık belirtin. Merhaba programını başlatın. Uzun süre çalışan API'ler kullanılacaktır.
6. Merhaba içeriğin yayımlanabilmesi ve tooyour istemcileri akışı hello varlık için bir Bulucu oluşturun.
7. Maskeleme görüntülerini gösterin ve gizleyin. Reklamları başlatın ve durdurun. Uzun süre çalışan API'ler kullanılacaktır.
8. Kanalınızı temizleyin ve tüm ilişkili kaynakları hello.

## <a name="prerequisites"></a>Ön koşullar
Merhaba, gerekli toocomplete hello öğretici verilmiştir.

* Bir Azure hesabı. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F). Out kullanılan tootry Ücretli Azure hizmetlerini olabilir krediler alırsınız. Hatta hello krediler bitmiş olsa, hello hesabı sürdürebilir ve ücretsiz Azure hizmetlerini ve Azure App Service Web Apps özelliğini hello gibi özellikleri kullanır.
* Bir Media Services hesabı. bir Media Services hesabı toocreate bkz [hesap oluştur](media-services-portal-create-account.md).
* Visual Studio 2010 SP1 (Professional, Premium, Ultimate veya Express) veya sonraki sürümleri.
* Media Services .NET SDK sürüm 3.2.0.0 veya daha yeni bir sürümünü kullanmanız gerekir.
* Bir web kamerası ve tek bit hızlı bir canlı akış gönderebilen bir kodlayıcı.

## <a name="considerations"></a>Dikkat edilmesi gerekenler
* Şu anda hello en fazla canlı bir olay süresi önerilen 8 saattir. Uzun süreyle toorun bir kanal gerekiyorsa lütfen amslived@Microsoft.com adresine başvurun.
* Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için). Merhaba kullanması gereken her zaman kullanıyorsanız, aynı ilke kimliği hello aynı gün / erişim izinlerini, örneğin, uzun bir süre (karşıya yükleme olmayan ilkeleri) yerinde hedeflenen tooremain olan bulucular ilkeleri. Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.

## <a name="download-sample"></a>Örnek indirme

Bu konudan açıklanan hello örnek indirebilirsiniz [burada](https://azure.microsoft.com/documentation/samples/media-services-dotnet-encode-live-stream-with-ams-clear/).

## <a name="set-up-for-development-with-media-services-sdk-for-net"></a>.NET için Media Services SDK ile geliştirme amaçlı ayarlama

Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md). 

## <a name="code-example"></a>Kod örneği

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Net;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace EncodeLiveStreamWithAmsClear
    {
        class Program
        {
        private const string ChannelName = "channel001";
        private const string AssetlName = "asset001";
        private const string ProgramlName = "program001";

        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            IChannel channel = CreateAndStartChannel();

            // hello channel's input endpoint:
            string ingestUrl = channel.Input.Endpoints.FirstOrDefault().Url.ToString();

            Console.WriteLine("Intest URL: {0}", ingestUrl);


            // Use hello previewEndpoint toopreview and verify 
            // that hello input from hello encoder is actually reaching hello Channel. 
            string previewEndpoint = channel.Preview.Endpoints.FirstOrDefault().Url.ToString();

            Console.WriteLine("Preview URL: {0}", previewEndpoint);

            // When Live Encoding is enabled, you can now get a preview of hello live feed as it reaches hello Channel. 
            // This can be a valuable tool toocheck whether your live feed is actually reaching hello Channel. 
            // hello thumbnail is exposed via hello same end-point as hello Channel Preview URL.
            string thumbnailUri = new UriBuilder
            {
            Scheme = Uri.UriSchemeHttps,
            Host = channel.Preview.Endpoints.FirstOrDefault().Url.Host,
            Path = "thumbnails/input.jpg"
            }.Uri.ToString();

            Console.WriteLine("Thumbain URL: {0}", thumbnailUri);

            // Once you previewed your stream and verified that it is flowing into your Channel, 
            // you can create an event by creating an Asset, Program, and Streaming Locator. 
            IAsset asset = CreateAndConfigureAsset();

            IProgram program = CreateAndStartProgram(channel, asset);

            ILocator locator = CreateLocatorForAsset(program.Asset, program.ArchiveWindowLength);

            // You can use slates and ads only if hello channel type is Standard.  
            StartStopAdsSlates(channel);

            // Once you are done streaming, clean up your resources.
            Cleanup(channel);
        }

        public static IChannel CreateAndStartChannel()
        {
            var channelInput = CreateChannelInput();
            var channePreview = CreateChannelPreview();
            var channelEncoding = CreateChannelEncoding();

            ChannelCreationOptions options = new ChannelCreationOptions
            {
            EncodingType = ChannelEncodingType.Standard,
            Name = ChannelName,
            Input = channelInput,
            Preview = channePreview,
            Encoding = channelEncoding
            };

            Log("Creating channel");
            IOperation channelCreateOperation = _context.Channels.SendCreateOperation(options);
            string channelId = TrackOperation(channelCreateOperation, "Channel create");

            IChannel channel = _context.Channels.Where(c => c.Id == channelId).FirstOrDefault();

            Log("Starting channel");
            var channelStartOperation = channel.SendStartOperation();
            TrackOperation(channelStartOperation, "Channel start");

            return channel;
        }

        /// <summary>
        /// Create channel input, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelInput CreateChannelInput()
        {
            return new ChannelInput
            {
            StreamingProtocol = StreamingProtocol.RTPMPEG2TS,
            AccessControl = new ChannelAccessControl
            {
                IPAllowList = new List<IPRange>
                {
                    new IPRange
                    {
                    Name = "TestChannelInput001",
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

        /// <summary>
        /// Create channel preview, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelPreview CreateChannelPreview()
        {
            return new ChannelPreview
            {
            AccessControl = new ChannelAccessControl
            {
                IPAllowList = new List<IPRange>
                {
                    new IPRange
                    {
                    Name = "TestChannelPreview001",
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

        /// <summary>
        /// Create channel encoding, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelEncoding CreateChannelEncoding()
        {
            return new ChannelEncoding
            {
            SystemPreset = "Default720p",
            IgnoreCea708ClosedCaptions = false,
            AdMarkerSource = AdMarkerSource.Api,
            // You can only set audio if streaming protocol is set tooStreamingProtocol.RTPMPEG2TS.
            AudioStreams = new List<AudioStream> { new AudioStream { Index = 103, Language = "eng" } }.AsReadOnly()
            };
        }

        /// <summary>
        /// Create an asset and configure asset delivery policies.
        /// </summary>
        /// <returns></returns>
        public static IAsset CreateAndConfigureAsset()
        {
            IAsset asset = _context.Assets.Create(AssetlName, AssetCreationOptions.None);

            IAssetDeliveryPolicy policy =
            _context.AssetDeliveryPolicies.Create("Clear Policy",
            AssetDeliveryPolicyType.NoDynamicEncryption,
            AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);

            asset.DeliveryPolicies.Add(policy);

            return asset;
        }

        /// <summary>
        /// Create a Program on hello Channel. You can have multiple Programs that overlap or are sequential;
        /// however each Program must have a unique name within your Media Services account.
        /// </summary>
        /// <param name="channel"></param>
        /// <param name="asset"></param>
        /// <returns></returns>
        public static IProgram CreateAndStartProgram(IChannel channel, IAsset asset)
        {
            IProgram program = channel.Programs.Create(ProgramlName, TimeSpan.FromHours(3), asset.Id);
            Log("Program created", program.Id);

            Log("Starting program");
            var programStartOperation = program.SendStartOperation();
            TrackOperation(programStartOperation, "Program start");

            return program;
        }

        /// <summary>
        /// Create locators in order toobe able toopublish and stream hello video.
        /// </summary>
        /// <param name="asset"></param>
        /// <param name="ArchiveWindowLength"></param>
        /// <returns></returns>
        public static ILocator CreateLocatorForAsset(IAsset asset, TimeSpan ArchiveWindowLength)
        {
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
            var locator = _context.Locators.CreateLocator
            (
                LocatorType.OnDemandOrigin,
                asset,
                _context.AccessPolicies.Create
                (
                    "Live Stream Policy",
                    ArchiveWindowLength,
                    AccessPermissions.Read
                )
            );

            return locator;
        }

        /// <summary>
        /// Perform operations on slates.
        /// </summary>
        /// <param name="channel"></param>
        public static void StartStopAdsSlates(IChannel channel)
        {
            int cueId = new Random().Next(int.MaxValue);
            var path = Path.GetFullPath(Path.Combine(AppDomain.CurrentDomain.BaseDirectory, @"..\\..\\SlateJPG\\DefaultAzurePortalSlate.jpg"));

            Log("Creating asset");
            var slateAsset = _context.Assets.Create("Slate test asset " + DateTime.Now.ToString("yyyy-MM-dd HH-mm"), AssetCreationOptions.None);
            Log("Slate asset created", slateAsset.Id);

            Log("Uploading file");
            var assetFile = slateAsset.AssetFiles.Create("DefaultAzurePortalSlate.jpg");
            assetFile.Upload(path);
            assetFile.IsPrimary = true;
            assetFile.Update();

            Log("Showing slate");
            var showSlateOpeartion = channel.SendShowSlateOperation(TimeSpan.FromMinutes(1), slateAsset.Id);
            TrackOperation(showSlateOpeartion, "Show slate");

            Log("Hiding slate");
            var hideSlateOperation = channel.SendHideSlateOperation();
            TrackOperation(hideSlateOperation, "Hide slate");

            Log("Starting ad");
            var startAdOperation = channel.SendStartAdvertisementOperation(TimeSpan.FromMinutes(1), cueId, false);
            TrackOperation(startAdOperation, "Start ad");

            Log("Ending ad");
            var endAdOperation = channel.SendEndAdvertisementOperation(cueId);
            TrackOperation(endAdOperation, "End ad");

            Log("Deleting slate asset");
            slateAsset.Delete();
        }

        /// <summary>
        /// Clean up resources associated with hello channel.
        /// </summary>
        /// <param name="channel"></param>
        public static void Cleanup(IChannel channel)
        {
            IAsset asset;
            if (channel != null)
            {
            foreach (var program in channel.Programs)
            {
                asset = _context.Assets.Where(se => se.Id == program.AssetId)
                            .FirstOrDefault();

                Log("Stopping program");
                var programStopOperation = program.SendStopOperation();
                TrackOperation(programStopOperation, "Program stop");

                program.Delete();

                if (asset != null)
                {
                Log("Deleting locators");
                foreach (var l in asset.Locators)
                    l.Delete();

                Log("Deleting asset");
                asset.Delete();
                }
            }

            Log("Stopping channel");
            var channelStopOperation = channel.SendStopOperation();
            TrackOperation(channelStopOperation, "Channel stop");

            Log("Deleting channel");
            var channelDeleteOperation = channel.SendDeleteOperation();
            TrackOperation(channelDeleteOperation, "Channel delete");
            }
        }

        /// <summary>
        /// Track long running operations.
        /// </summary>
        /// <param name="operation"></param>
        /// <param name="description"></param>
        /// <returns></returns>
        public static string TrackOperation(IOperation operation, string description)
        {
            string entityId = null;
            bool isCompleted = false;

            Log("starting tootrack ", null, operation.Id);
            while (isCompleted == false)
            {
            operation = _context.Operations.GetOperation(operation.Id);
            isCompleted = IsCompleted(operation, out entityId);
            System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
            }
            // If we got here, hello operation succeeded.
            Log(description + " in completed", operation.TargetEntityId, operation.Id);

            return entityId;
        }

        /// <summary> 
        /// Checks if hello operation has been completed. 
        /// If hello operation succeeded, hello created entity Id is returned in hello out parameter.
        /// </summary> 
        /// <param name="operationId">hello operation Id.</param> 
        /// <param name="channel">
        /// If hello operation succeeded, 
        /// hello entity Id associated with hello sucessful operation is returned in hello out parameter.</param>
        /// <returns>Returns false if hello operation is still in progress; otherwise, true.</returns> 
        private static bool IsCompleted(IOperation operation, out string entityId)
        {
            bool completed = false;

            entityId = null;

            switch (operation.State)
            {
            case OperationState.Failed:
                // Handle hello failure. 
                // For example, throw an exception. 
                // Use hello following information in hello exception: operationId, operation.ErrorMessage.
                Log("operation failed", operation.TargetEntityId, operation.Id);
                break;
            case OperationState.Succeeded:
                completed = true;
                entityId = operation.TargetEntityId;
                break;
            case OperationState.InProgress:
                completed = false;
                Log("operation in progress", operation.TargetEntityId, operation.Id);
                break;
            }
            return completed;
        }

        private static void Log(string action, string entityId = null, string operationId = null)
        {
            Console.WriteLine(
            "{0,-21}{1,-51}{2,-51}{3,-51}",
            DateTime.Now.ToString("yyyy'-'MM'-'dd HH':'mm':'ss"),
            action,
            entityId ?? string.Empty,
            operationId ?? string.Empty);
        }
        }
    }

## <a name="next-step"></a>Sonraki adım
Media Services öğrenme yollarını gözden geçirin.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


