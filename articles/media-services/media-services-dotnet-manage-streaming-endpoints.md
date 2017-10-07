---
title: "Akış uç noktaları .NET SDK'sı aaaManage. | Microsoft Belgeleri"
description: "Bu konu, nasıl Azure portal ile toomanage akış uç noktalarını hello gösterir."
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: 0da34a97-f36c-48d0-8ea2-ec12584a2215
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 30c092a8ebf4e2b2902392f4cf98f46d812ccdbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-net-sdk"></a><span data-ttu-id="4d88a-104">.NET SDK'sı akış uç noktalarını yönetme</span><span class="sxs-lookup"><span data-stu-id="4d88a-104">Manage streaming endpoints with .NET SDK</span></span>

>[!NOTE]
><span data-ttu-id="4d88a-105">Tooreview hello emin olun [genel bakış](media-services-streaming-endpoints-overview.md) konu.</span><span class="sxs-lookup"><span data-stu-id="4d88a-105">Make sure tooreview hello [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> <span data-ttu-id="4d88a-106">Ayrıca, gözden [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="4d88a-106">Also, review [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="4d88a-107">Bu konudaki Hello kod nasıl toodo hello kullanarak görevleri aşağıdaki hello Azure Media Services .NET SDK'sı gösterir:</span><span class="sxs-lookup"><span data-stu-id="4d88a-107">hello code in this topic shows how toodo hello following tasks using hello Azure Media Services .NET SDK:</span></span>

- <span data-ttu-id="4d88a-108">Merhaba varsayılan akış uç noktası inceleyin.</span><span class="sxs-lookup"><span data-stu-id="4d88a-108">Examine hello default streaming endpoint.</span></span>
- <span data-ttu-id="4d88a-109">Oluşturma/yeni akış uç noktası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4d88a-109">Create/add new streaming endpoint.</span></span>

    <span data-ttu-id="4d88a-110">Toohave düşünüyorsanız, birden çok akış uç noktalarını toohave isteyebilirsiniz farklı CDN'ler veya CDN ve doğrudan erişim.</span><span class="sxs-lookup"><span data-stu-id="4d88a-110">You might want toohave multiple streaming endpoints if you plan toohave different CDNs or a CDN and direct access.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4d88a-111">Akış uç noktanızı çalışır durumda olduğunda yalnızca faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="4d88a-111">You are only billed when your Streaming Endpoint is in running state.</span></span>
    
- <span data-ttu-id="4d88a-112">Akış uç noktası hello güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="4d88a-112">Update hello streaming endpoint.</span></span>
    
    <span data-ttu-id="4d88a-113">Toocall hello Update() işlevi emin olun.</span><span class="sxs-lookup"><span data-stu-id="4d88a-113">Make sure toocall hello Update() function.</span></span>

- <span data-ttu-id="4d88a-114">Akış uç noktası hello silin.</span><span class="sxs-lookup"><span data-stu-id="4d88a-114">Delete hello streaming endpoint.</span></span>

    >[!NOTE]
    ><span data-ttu-id="4d88a-115">Merhaba varsayılan akış uç noktası silinemiyor.</span><span class="sxs-lookup"><span data-stu-id="4d88a-115">hello default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="4d88a-116">Nasıl tooscale hello akış uç noktası hakkında daha fazla bilgi için bkz: [bu](media-services-portal-scale-streaming-endpoints.md) konu.</span><span class="sxs-lookup"><span data-stu-id="4d88a-116">For information about how tooscale hello streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="4d88a-117">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4d88a-117">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="4d88a-118">Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="4d88a-118">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="add-code-that-manages-streaming-endpoints"></a><span data-ttu-id="4d88a-119">Akış uç noktalarını yönetir kodu ekleyin</span><span class="sxs-lookup"><span data-stu-id="4d88a-119">Add code that manages streaming endpoints</span></span>
    
<span data-ttu-id="4d88a-120">Merhaba Program.cs Hello kodda koddan hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4d88a-120">Replace hello code in hello Program.cs with hello following code:</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.Live;

    namespace AMSStreamingEndpoint
    {
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
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            var defaultStreamingEndpoint = _context.StreamingEndpoints.Where(s => s.Name.Contains("default")).FirstOrDefault();
            ExamineStreamingEndpoint(defaultStreamingEndpoint);

            IStreamingEndpoint newStreamingEndpoint = AddStreamingEndpoint();
            UpdateStreamingEndpoint(newStreamingEndpoint);
            DeleteStreamingEndpoint(newStreamingEndpoint);
        }

        static public void ExamineStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            Console.WriteLine(streamingEndpoint.Name);
            Console.WriteLine(streamingEndpoint.StreamingEndpointVersion);
            Console.WriteLine(streamingEndpoint.FreeTrialEndTime);
            Console.WriteLine(streamingEndpoint.ScaleUnits);
            Console.WriteLine(streamingEndpoint.CdnProvider);
            Console.WriteLine(streamingEndpoint.CdnProfile);
            Console.WriteLine(streamingEndpoint.CdnEnabled);
        }

        static public IStreamingEndpoint AddStreamingEndpoint()
        {
            var name = "StreamingEndpoint" + DateTime.UtcNow.ToString("hhmmss");
            var option = new StreamingEndpointCreationOptions(name, 1)
            {
            StreamingEndpointVersion = new Version("2.0"),
            CdnEnabled = true,
            CdnProfile = "CdnProfile",
            CdnProvider = CdnProviderType.PremiumVerizon
            };

            var streamingEndpoint = _context.StreamingEndpoints.Create(option);

            return streamingEndpoint;
        }

        static public void UpdateStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            if (streamingEndpoint.StreamingEndpointVersion == "1.0")
            streamingEndpoint.StreamingEndpointVersion = "2.0";

            streamingEndpoint.CdnEnabled = false;
            streamingEndpoint.Update();
        }

        static public void DeleteStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            streamingEndpoint.Delete();
        }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="4d88a-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4d88a-121">Next steps</span></span>
<span data-ttu-id="4d88a-122">Media Services öğrenme yollarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="4d88a-122">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4d88a-123">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="4d88a-123">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

