---
title: .NET ile Azure Media Services telemetri aaaConfiguring | Microsoft Docs
description: "Bu makalede nasıl toouse hello .NET SDK kullanarak Azure Media Services telemetri gösterilmektedir."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f8f55e37-0714-49ea-bf4a-e6c1319bec44
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 4019fa7d080ca3f8a8709bd1e666f7062b883954
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-azure-media-services-telemetry-with-net"></a><span data-ttu-id="c895d-103">.NET ile Azure Media Services telemetri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c895d-103">Configuring Azure Media Services telemetry with .NET</span></span>

<span data-ttu-id="c895d-104">Bu konuda, .NET SDK kullanarak Azure Media Services (AMS) telemetri hello yapılandırırken sürebilir genel adımlar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c895d-104">This topic describes general steps that you might take when configuring hello Azure Media Services (AMS) telemetry using .NET SDK.</span></span> 

>[!NOTE]
><span data-ttu-id="c895d-105">Merhaba ne ayrıntılı bir açıklama AMS telemetri için ve nasıl tooconsume, hello bkz [genel bakış](media-services-telemetry-overview.md) konu.</span><span class="sxs-lookup"><span data-stu-id="c895d-105">For hello detailed explanation of what is AMS telemetry and how tooconsume it, see hello [overview](media-services-telemetry-overview.md) topic.</span></span>

<span data-ttu-id="c895d-106">Telemetri verileri yolları aşağıdaki hello birinde kullanmasını sağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c895d-106">You can consume telemetry data in one of hello following ways:</span></span>

- <span data-ttu-id="c895d-107">Verileri doğrudan Azure Table (örneğin hello depolama SDK'sını kullanarak) depolama alanından okuyun.</span><span class="sxs-lookup"><span data-stu-id="c895d-107">Read data directly from Azure Table Storage (e.g. using hello Storage SDK).</span></span> <span data-ttu-id="c895d-108">Merhaba telemetri depolama tabloları Hello açıklaması için bkz **telemetri bilgileri tüketen** içinde [bu](https://msdn.microsoft.com/library/mt742089.aspx) konu.</span><span class="sxs-lookup"><span data-stu-id="c895d-108">For hello description of telemetry storage tables, see hello **Consuming telemetry information** in [this](https://msdn.microsoft.com/library/mt742089.aspx) topic.</span></span>

<span data-ttu-id="c895d-109">Veya</span><span class="sxs-lookup"><span data-stu-id="c895d-109">Or</span></span>

- <span data-ttu-id="c895d-110">Depolama verileri okumak için Media Services .NET SDK'sı hello kullan hello desteği.</span><span class="sxs-lookup"><span data-stu-id="c895d-110">Use hello support in hello Media Services .NET SDK for reading storage data.</span></span> <span data-ttu-id="c895d-111">Bu konu, hello tooenable telemetri AMS hesabının nasıl belirtilen ve nasıl tooquery hello ölçümleri kullanarak Azure Media Services .NET SDK'sı hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="c895d-111">This topic shows how tooenable telemetry for hello specified AMS account and how tooquery hello metrics using hello Azure Media Services .NET SDK.</span></span>  

## <a name="configuring-telemetry-for-a-media-services-account"></a><span data-ttu-id="c895d-112">Telemetri bir Media Services hesabı için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c895d-112">Configuring telemetry for a Media Services account</span></span>

<span data-ttu-id="c895d-113">Merhaba aşağıdaki adımlar gerekli tooenable telemetri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c895d-113">hello following steps are needed tooenable telemetry:</span></span>

- <span data-ttu-id="c895d-114">Merhaba depolama hesabı bağlı toohello Media Services hesabı Hello kimlik bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="c895d-114">Get hello credentials of hello storage account attached toohello Media Services account.</span></span> 
- <span data-ttu-id="c895d-115">Bildirim uç noktası ile oluşturma **EndPointType** çok ayarlamak**AzureTable** ve toohello depolama tablosu işaret eden endPointAddress.</span><span class="sxs-lookup"><span data-stu-id="c895d-115">Create a Notification Endpoint with **EndPointType** set too**AzureTable** and endPointAddress pointing toohello storage table.</span></span>

        INotificationEndPoint notificationEndPoint = 
                      _context.NotificationEndPoints.Create("monitoring", 
                      NotificationEndPointType.AzureTable,
                      "https://" + _mediaServicesStorageAccountName + ".table.core.windows.net/");

- <span data-ttu-id="c895d-116">Merhaba, hizmetleri için izleme yapılandırma ayarları oluştur toomonitor istiyor.</span><span class="sxs-lookup"><span data-stu-id="c895d-116">Create a monitoring configuration settings for hello services you want toomonitor.</span></span> <span data-ttu-id="c895d-117">Birden fazla yapılandırma ayarları izleme izin verilir.</span><span class="sxs-lookup"><span data-stu-id="c895d-117">No more than one monitoring configuration settings is allowed.</span></span> 
  
        IMonitoringConfiguration monitoringConfiguration = _context.MonitoringConfigurations.Create(notificationEndPoint.Id,
            new List<ComponentMonitoringSetting>()
            {
                new ComponentMonitoringSetting(MonitoringComponent.Channel, MonitoringLevel.Normal),
                new ComponentMonitoringSetting(MonitoringComponent.StreamingEndpoint, MonitoringLevel.Normal)
            });

## <a name="consuming-telemetry-information"></a><span data-ttu-id="c895d-118">Telemetri bilgileri kullanma</span><span class="sxs-lookup"><span data-stu-id="c895d-118">Consuming telemetry information</span></span>

<span data-ttu-id="c895d-119">Süren telemetri bilgileri hakkında daha fazla bilgi için bkz: [bu](media-services-telemetry-overview.md) konu.</span><span class="sxs-lookup"><span data-stu-id="c895d-119">For information about consuming telemetry information, see [this](media-services-telemetry-overview.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="c895d-120">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c895d-120">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="c895d-121">Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="c895d-121">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

2. <span data-ttu-id="c895d-122">Öğe çok aşağıdaki hello eklemek**appSettings** app.config dosyasında tanımlanan:</span><span class="sxs-lookup"><span data-stu-id="c895d-122">Add hello following element too**appSettings** defined in your app.config file:</span></span>

    <add key="StorageAccountName" value="storage_name" />
 
## <a name="example"></a><span data-ttu-id="c895d-123">Örnek</span><span class="sxs-lookup"><span data-stu-id="c895d-123">Example</span></span>  
    
<span data-ttu-id="c895d-124">Aşağıdaki örneğine hello hello tooenable telemetri AMS hesabının nasıl belirtilen ve nasıl tooquery hello ölçümleri kullanarak Azure Media Services .NET SDK'sı hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="c895d-124">hello following example shows how tooenable telemetry for hello specified AMS account and how tooquery hello metrics using hello Azure Media Services .NET SDK.</span></span>  

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;

    namespace AMSMetrics
    {
        class Program
        {
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly string _mediaServicesStorageAccountName =
            ConfigurationManager.AppSettings["StorageAccountName"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static IStreamingEndpoint _streamingEndpoint = null;
        private static IChannel _channel = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            _streamingEndpoint = _context.StreamingEndpoints.FirstOrDefault();
            _channel = _context.Channels.FirstOrDefault();

            var monitoringConfigurations = _context.MonitoringConfigurations;
            IMonitoringConfiguration monitoringConfiguration = null;

            // No more than one monitoring configuration settings is allowed.
            if (monitoringConfigurations.ToArray().Length != 0)
            {
            monitoringConfiguration = _context.MonitoringConfigurations.FirstOrDefault();
            }
            else
            {
            INotificationEndPoint notificationEndPoint =
                      _context.NotificationEndPoints.Create("monitoring",
                      NotificationEndPointType.AzureTable, GetTableEndPoint());

            monitoringConfiguration = _context.MonitoringConfigurations.Create(notificationEndPoint.Id,
                new List<ComponentMonitoringSetting>()
                {
                    new ComponentMonitoringSetting(MonitoringComponent.Channel, MonitoringLevel.Normal),
                    new ComponentMonitoringSetting(MonitoringComponent.StreamingEndpoint, MonitoringLevel.Normal)

                });
            }

            //Print metrics for a Streaming Endpoint.
            PrintStreamingEndpointMetrics();

            Console.ReadLine();
        }

        private static string GetTableEndPoint()
        {
            return "https://" + _mediaServicesStorageAccountName + ".table.core.windows.net/";
        }

        private static void PrintStreamingEndpointMetrics()
        {
            Console.WriteLine(string.Format("Telemetry for streaming endpoint '{0}'", _streamingEndpoint.Name));

            DateTime timerangeEnd = DateTime.UtcNow;
            DateTime timerangeStart = DateTime.UtcNow.AddHours(-5);

            // Get some streaming endpoint metrics.
            var telemetry = _streamingEndpoint.GetTelemetry();

            var res = telemetry.GetStreamingEndpointRequestLogs(timerangeStart, timerangeEnd);

            Console.Title = "Streaming endpoint metrics:";

            foreach (var log in res)
            {
            Console.WriteLine("AccountId: {0}", log.AccountId);
            Console.WriteLine("BytesSent: {0}", log.BytesSent);
            Console.WriteLine("EndToEndLatency: {0}", log.EndToEndLatency);
            Console.WriteLine("HostName: {0}", log.HostName);
            Console.WriteLine("ObservedTime: {0}", log.ObservedTime);
            Console.WriteLine("PartitionKey: {0}", log.PartitionKey);
            Console.WriteLine("RequestCount: {0}", log.RequestCount);
            Console.WriteLine("ResultCode: {0}", log.ResultCode);
            Console.WriteLine("RowKey: {0}", log.RowKey);
            Console.WriteLine("ServerLatency: {0}", log.ServerLatency);
            Console.WriteLine("StatusCode: {0}", log.StatusCode);
            Console.WriteLine("StreamingEndpointId: {0}", log.StreamingEndpointId);
            Console.WriteLine();
            }

            Console.WriteLine();
        }

        private static void PrintChannelMetrics()
        {
            if (_channel == null)
            {
            Console.WriteLine("There are no channels in this AMS account");
            return;
            }

            Console.WriteLine(string.Format("Telemetry for channel '{0}'", _channel.Name));

            DateTime timerangeEnd = DateTime.UtcNow; 
            DateTime timerangeStart = DateTime.UtcNow.AddHours(-5);

            // Get some channel metrics.
            var telemetry = _channel.GetTelemetry();

            var channelMetrics = telemetry.GetChannelHeartbeats(timerangeStart, timerangeEnd);

            // Print hello channel metrics.
            Console.WriteLine("Channel metrics:");

            foreach (var channelHeartbeat in channelMetrics.OrderBy(x => x.ObservedTime))
            {
            Console.WriteLine(
                "    Observed time: {0}, Last timestamp: {1}, Incoming bitrate: {2}",
                channelHeartbeat.ObservedTime,
                channelHeartbeat.LastTimestamp,
                channelHeartbeat.IncomingBitrate);
            }

            Console.WriteLine();
        }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="c895d-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c895d-125">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c895d-126">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="c895d-126">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
