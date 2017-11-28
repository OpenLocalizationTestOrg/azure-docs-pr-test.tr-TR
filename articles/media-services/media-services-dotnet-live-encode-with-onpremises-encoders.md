---
title: "aaaHow tooperform Canlı ile akış içi .NET kullanarak kodlayıcılar | Microsoft Docs"
description: "Bu konu nasıl toouse .NET tooperform Canlı kodlama ile şirket içi kodlayıcılardan gösterir."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 15908152-d23c-4d55-906a-3bfd74927db5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 07/18/2017
ms.author: cenkdin;juliako
ms.openlocfilehash: 332582c9f925f8b9270929b3fa8140fce010bbf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-with-on-premises-encoders-using-net"></a><span data-ttu-id="8f4e4-103">Nasıl tooperform canlı akış .NET kullanarak şirket içi kodlayıcılarda</span><span class="sxs-lookup"><span data-stu-id="8f4e4-103">How tooperform live streaming with on-premises encoders using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8f4e4-104">Portal</span><span class="sxs-lookup"><span data-stu-id="8f4e4-104">Portal</span></span>](media-services-portal-live-passthrough-get-started.md)
> * [<span data-ttu-id="8f4e4-105">.NET</span><span class="sxs-lookup"><span data-stu-id="8f4e4-105">.NET</span></span>](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [<span data-ttu-id="8f4e4-106">REST</span><span class="sxs-lookup"><span data-stu-id="8f4e4-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="8f4e4-107">Bu öğretici, hello Azure Media Services .NET SDK'sı toocreate kullanmanın hello adımlarda size bir **kanal** doğrudan teslimat için yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="8f4e4-107">This tutorial walks you through hello steps of using hello Azure Media Services .NET SDK toocreate a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8f4e4-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8f4e4-108">Prerequisites</span></span>
<span data-ttu-id="8f4e4-109">Merhaba, gerekli toocomplete hello öğretici şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8f4e4-109">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="8f4e4-110">Bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="8f4e4-110">An Azure account.</span></span>
* <span data-ttu-id="8f4e4-111">Bir Media Services hesabı.</span><span class="sxs-lookup"><span data-stu-id="8f4e4-111">A Media Services account.</span></span>    <span data-ttu-id="8f4e4-112">bir Media Services hesabı toocreate bkz [nasıl tooCreate Media Services hesabı](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="8f4e4-112">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="8f4e4-113">Geliştirme ortamınızı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8f4e4-113">Set up your dev environment.</span></span> <span data-ttu-id="8f4e4-114">Daha fazla bilgi için bkz: [ortamınızı ayarlama](media-services-set-up-computer.md).</span><span class="sxs-lookup"><span data-stu-id="8f4e4-114">For more information, see [Set up your environment](media-services-set-up-computer.md).</span></span>
* <span data-ttu-id="8f4e4-115">Bir Web kamerası.</span><span class="sxs-lookup"><span data-stu-id="8f4e4-115">A webcam.</span></span> <span data-ttu-id="8f4e4-116">Örneğin, [Telestream Wirecast kodlayıcı](http://www.telestream.net/wirecast/overview.htm).</span><span class="sxs-lookup"><span data-stu-id="8f4e4-116">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="8f4e4-117">Önerilen tooreview hello makaleler:</span><span class="sxs-lookup"><span data-stu-id="8f4e4-117">Recommended tooreview hello following articles:</span></span>

* [<span data-ttu-id="8f4e4-118">Azure Media Services RTMP Desteği ve Gerçek Zamanlı Kodlayıcılar</span><span class="sxs-lookup"><span data-stu-id="8f4e4-118">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="8f4e4-119">Çoklu bit hızı akışları oluşturan şirket içi kodlayıcılarla canlı akış</span><span class="sxs-lookup"><span data-stu-id="8f4e4-119">Live streaming with on-premises encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="8f4e4-120">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8f4e4-120">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="8f4e4-121">Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="8f4e4-121">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="example"></a><span data-ttu-id="8f4e4-122">Örnek</span><span class="sxs-lookup"><span data-stu-id="8f4e4-122">Example</span></span>
<span data-ttu-id="8f4e4-123">Aşağıdaki kod örneğine hello nasıl tooachieve hello aşağıdaki görevleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="8f4e4-123">hello following code example demonstrates how tooachieve hello following tasks:</span></span>

* <span data-ttu-id="8f4e4-124">TooMedia Hizmetleri'ne Bağlama</span><span class="sxs-lookup"><span data-stu-id="8f4e4-124">Connect tooMedia Services</span></span>
* <span data-ttu-id="8f4e4-125">Kanal oluşturma</span><span class="sxs-lookup"><span data-stu-id="8f4e4-125">Create a channel</span></span>
* <span data-ttu-id="8f4e4-126">Güncelleştirme hello kanalı</span><span class="sxs-lookup"><span data-stu-id="8f4e4-126">Update hello channel</span></span>
* <span data-ttu-id="8f4e4-127">Merhaba kanalın giriş uç noktası alamadı.</span><span class="sxs-lookup"><span data-stu-id="8f4e4-127">Retrieve hello channel’s input endpoint.</span></span> <span data-ttu-id="8f4e4-128">Merhaba giriş uç noktası toohello içi gerçek zamanlı Kodlayıcı sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8f4e4-128">hello input endpoint should be provided toohello on-premises live encoder.</span></span> <span data-ttu-id="8f4e4-129">Merhaba gerçek zamanlı Kodlayıcı dönüştürür sinyalleri toohello kanalın giriş gönderilen hello kamera toostreams gelen (uç noktasını alın).</span><span class="sxs-lookup"><span data-stu-id="8f4e4-129">hello live encoder converts signals from hello camera toostreams that are sent toohello channel’s input (ingest) endpoint.</span></span>
* <span data-ttu-id="8f4e4-130">Merhaba kanalın Önizleme uç noktasını alın</span><span class="sxs-lookup"><span data-stu-id="8f4e4-130">Retrieve hello channel’s preview endpoint</span></span>
* <span data-ttu-id="8f4e4-131">Oluşturma ve bir program başlatma</span><span class="sxs-lookup"><span data-stu-id="8f4e4-131">Create and start a program</span></span>
* <span data-ttu-id="8f4e4-132">Tooaccess program hello bir Bulucu oluşturun</span><span class="sxs-lookup"><span data-stu-id="8f4e4-132">Create a locator needed tooaccess hello program</span></span>
* <span data-ttu-id="8f4e4-133">Oluşturma ve bir StreamingEndpoint başlatma</span><span class="sxs-lookup"><span data-stu-id="8f4e4-133">Create and start a StreamingEndpoint</span></span>
* <span data-ttu-id="8f4e4-134">Akış uç noktası hello güncelleştir</span><span class="sxs-lookup"><span data-stu-id="8f4e4-134">Update hello streaming endpoint</span></span>
* <span data-ttu-id="8f4e4-135">Kapatma kaynakları</span><span class="sxs-lookup"><span data-stu-id="8f4e4-135">Shut down resources</span></span>

>[!IMPORTANT]
><span data-ttu-id="8f4e4-136">Akış uç noktası toostream içerik istediğiniz hello hello olduğundan emin olun **çalıştıran** durumu.</span><span class="sxs-lookup"><span data-stu-id="8f4e4-136">Make sure hello streaming endpoint from which you want toostream content is in hello **Running** state.</span></span> 
    
>[!NOTE]
><span data-ttu-id="8f4e4-137">Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için).</span><span class="sxs-lookup"><span data-stu-id="8f4e4-137">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="8f4e4-138">Merhaba kullanması gereken her zaman kullanıyorsanız, aynı ilke kimliği hello aynı gün / erişim izinlerini, örneğin, uzun bir süre (karşıya yükleme olmayan ilkeleri) yerinde hedeflenen tooremain olan bulucular ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="8f4e4-138">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="8f4e4-139">Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="8f4e4-139">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="8f4e4-140">Hakkında bilgi için bkz tooconfigure gerçek zamanlı Kodlayıcı [Azure Media Services RTMP desteği ve gerçek zamanlı kodlayıcılar](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/).</span><span class="sxs-lookup"><span data-stu-id="8f4e4-140">For information on how tooconfigure a live encoder, see [Azure Media Services RTMP Support and Live Encoders](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/).</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Linq;
    using System.Net;
    using System.Security.Cryptography;
    using Microsoft.WindowsAzure.MediaServices.Client;

    namespace AMSLiveTest
    {
        class Program
        {
        private const string StreamingEndpointName = "streamingendpoint001";
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

            // Set hello Live Encoder toopoint toohello channel's input endpoint:
            string ingestUrl = channel.Input.Endpoints.FirstOrDefault().Url.ToString();

            // Use hello previewEndpoint toopreview and verify
            // that hello input from hello encoder is actually reaching hello Channel.
            string previewEndpoint = channel.Preview.Endpoints.FirstOrDefault().Url.ToString();

            IProgram program = CreateAndStartProgram(channel);
            ILocator locator = CreateLocatorForAsset(program.Asset, program.ArchiveWindowLength);
            IStreamingEndpoint streamingEndpoint = CreateAndStartStreamingEndpoint(false);

            // Once you are done streaming, clean up your resources.
            Cleanup(streamingEndpoint, channel);
        }

        public static IChannel CreateAndStartChannel()
        {
            //If you want toochange hello Smooth fragments tooHLS segment ratio, you would set hello ChannelCreationOptions’s Output property.

            IChannel channel = _context.Channels.Create(
            new ChannelCreationOptions
            {
            Name = ChannelName,
            Input = CreateChannelInput(),
            Preview = CreateChannelPreview()
            });

            //Starting and stopping Channels can take some time tooexecute. toodetermine hello state of operations after calling Start or Stop, query hello IChannel.State .

            channel.Start();

            return channel;
        }

        private static ChannelInput CreateChannelInput()
        {
            return new ChannelInput
            {
            StreamingProtocol = StreamingProtocol.RTMP,
            AccessControl = new ChannelAccessControl
            {
                IPAllowList = new List<IPRange>
                    {
                    new IPRange
                    {
                    Name = "TestChannelInput001",
                    // Setting 0.0.0.0 for Address and 0 for SubnetPrefixLength
                    // will allow access tooIP addresses.
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

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
                    // Setting 0.0.0.0 for Address and 0 for SubnetPrefixLength
                    // will allow access tooIP addresses.
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

        public static void UpdateCrossSiteAccessPoliciesForChannel(IChannel channel)
        {
            var clientPolicy =
            @"<?xml version=""1.0"" encoding=""utf-8""?>
            <access-policy>
                <cross-domain-access>
                <policy>
                    <allow-from http-request-headers=""*"" http-methods=""*"">
                    <domain uri=""*""/>
                    </allow-from>
                    <grant-to>
                       <resource path=""/"" include-subpaths=""true""/>
                    </grant-to>
                </policy>
                </cross-domain-access>
            </access-policy>";

            var xdomainPolicy =
            @"<?xml version=""1.0"" ?>
            <cross-domain-policy>
                <allow-access-from domain=""*"" />
            </cross-domain-policy>";

            channel.CrossSiteAccessPolicies.ClientAccessPolicy = clientPolicy;
            channel.CrossSiteAccessPolicies.CrossDomainPolicy = xdomainPolicy;

            channel.Update();
        }

        public static IProgram CreateAndStartProgram(IChannel channel)
        {
            IAsset asset = _context.Assets.Create(AssetlName, AssetCreationOptions.None);

            // Create a Program on hello Channel. You can have multiple Programs that overlap or are sequential;
            // however each Program must have a unique name within your Media Services account.
            IProgram program = channel.Programs.Create(ProgramlName, TimeSpan.FromHours(3), asset.Id);
            program.Start();

            return program;
        }

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

        public static IStreamingEndpoint CreateAndStartStreamingEndpoint(bool createNew)
        {
            IStreamingEndpoint streamingEndpoint = null;
            if (createNew)
            {
            var options = new StreamingEndpointCreationOptions
            {
                Name = StreamingEndpointName,
                ScaleUnits = 1,
                AccessControl = GetAccessControl(),
                CacheControl = GetCacheControl()
            };

            streamingEndpoint = _context.StreamingEndpoints.Create(options);
            }
            else
            {
            streamingEndpoint = _context.StreamingEndpoints.FirstOrDefault();
            }


            if (streamingEndpoint.State == StreamingEndpointState.Stopped)
            streamingEndpoint.Start();

            return streamingEndpoint;
        }

        private static StreamingEndpointAccessControl GetAccessControl()
        {
            return new StreamingEndpointAccessControl
            {
            IPAllowList = new List<IPRange>
                {
                new IPRange
                {
                    Name = "Allow all",
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                }
                },

            AkamaiSignatureHeaderAuthenticationKeyList = new List<AkamaiSignatureHeaderAuthenticationKey>
                {
                new AkamaiSignatureHeaderAuthenticationKey
                {
                    Identifier = "My key",
                    Expiration = DateTime.UtcNow + TimeSpan.FromDays(365),
                    Base64Key = Convert.ToBase64String(GenerateRandomBytes(16))
                }
                }
            };
        }

        private static byte[] GenerateRandomBytes(int length)
        {
            var bytes = new byte[length];
            using (var rng = new RNGCryptoServiceProvider())
            {
            rng.GetBytes(bytes);
            }

            return bytes;
        }

        private static StreamingEndpointCacheControl GetCacheControl()
        {
            return new StreamingEndpointCacheControl
            {
            MaxAge = TimeSpan.FromSeconds(1000)
            };
        }

        public static void UpdateCrossSiteAccessPoliciesForStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            var clientPolicy =
            @"<?xml version=""1.0"" encoding=""utf-8""?>
            <access-policy>
                <cross-domain-access>
                <policy>
                    <allow-from http-request-headers=""*"" http-methods=""*"">
                    <domain uri=""*""/>
                    </allow-from>
                    <grant-to>
                       <resource path=""/"" include-subpaths=""true""/>
                    </grant-to>
                </policy>
                </cross-domain-access>
            </access-policy>";

            var xdomainPolicy =
            @"<?xml version=""1.0"" ?>
            <cross-domain-policy>
                <allow-access-from domain=""*"" />
            </cross-domain-policy>";

            streamingEndpoint.CrossSiteAccessPolicies.ClientAccessPolicy = clientPolicy;
            streamingEndpoint.CrossSiteAccessPolicies.CrossDomainPolicy = xdomainPolicy;

            streamingEndpoint.Update();
        }

        public static void Cleanup(IStreamingEndpoint streamingEndpoint,
                        IChannel channel)
        {
            if (streamingEndpoint != null)
            {
            streamingEndpoint.Stop();
            if(streamingEndpoint.Name != "default")
                streamingEndpoint.Delete();
            }

            IAsset asset;
            if (channel != null)
            {

            foreach (var program in channel.Programs)
            {
                asset = _context.Assets.Where(se => se.Id == program.AssetId)
                            .FirstOrDefault();

                program.Stop();
                program.Delete();

                if (asset != null)
                {
                foreach (var l in asset.Locators)
                    l.Delete();

                asset.Delete();
                }
            }

            channel.Stop();
            channel.Delete();
            }
        }
        }
    }

## <a name="next-step"></a><span data-ttu-id="8f4e4-141">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="8f4e4-141">Next Step</span></span>
<span data-ttu-id="8f4e4-142">Gözden geçirme Media Services'i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="8f4e4-142">Review Media Services learning paths</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8f4e4-143">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="8f4e4-143">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

