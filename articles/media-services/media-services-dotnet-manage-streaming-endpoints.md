---
title: ".NET SDK'sı akış uç noktalarını yönetin. | Microsoft Belgeleri"
description: "Bu konu Azure portal ile akış uç noktalarını yönetme gösterir."
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
ms.openlocfilehash: 2f4f464f8604b6f453d6b50b736c6a3a889a3408
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-streaming-endpoints-with-net-sdk"></a><span data-ttu-id="33e75-104">.NET SDK'sı akış uç noktalarını yönetme</span><span class="sxs-lookup"><span data-stu-id="33e75-104">Manage streaming endpoints with .NET SDK</span></span>

>[!NOTE]
><span data-ttu-id="33e75-105">Gözden geçirdiğinizden emin olun [genel bakış](media-services-streaming-endpoints-overview.md) konu.</span><span class="sxs-lookup"><span data-stu-id="33e75-105">Make sure to review the [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> <span data-ttu-id="33e75-106">Ayrıca, gözden [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="33e75-106">Also, review [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="33e75-107">Bu konudaki kod Azure Media Services .NET SDK kullanarak aşağıdaki görevlerin nasıl yapılacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="33e75-107">The code in this topic shows how to do the following tasks using the Azure Media Services .NET SDK:</span></span>

- <span data-ttu-id="33e75-108">Varsayılan akış uç inceleyin.</span><span class="sxs-lookup"><span data-stu-id="33e75-108">Examine the default streaming endpoint.</span></span>
- <span data-ttu-id="33e75-109">Oluşturma/yeni akış uç noktası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="33e75-109">Create/add new streaming endpoint.</span></span>

    <span data-ttu-id="33e75-110">Farklı CDN'ler veya CDN ve doğrudan erişimi olmasını planlıyorsanız, birden çok akış uç noktalarını sahip olmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33e75-110">You might want to have multiple streaming endpoints if you plan to have different CDNs or a CDN and direct access.</span></span>

    > [!NOTE]
    > <span data-ttu-id="33e75-111">Akış uç noktanızı çalışır durumda olduğunda yalnızca faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="33e75-111">You are only billed when your Streaming Endpoint is in running state.</span></span>
    
- <span data-ttu-id="33e75-112">Akış uç noktasını güncelleyin.</span><span class="sxs-lookup"><span data-stu-id="33e75-112">Update the streaming endpoint.</span></span>
    
    <span data-ttu-id="33e75-113">Update() işlevi çağırdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="33e75-113">Make sure to call the Update() function.</span></span>

- <span data-ttu-id="33e75-114">Akış uç silin.</span><span class="sxs-lookup"><span data-stu-id="33e75-114">Delete the streaming endpoint.</span></span>

    >[!NOTE]
    ><span data-ttu-id="33e75-115">Varsayılan akış uç silinemiyor.</span><span class="sxs-lookup"><span data-stu-id="33e75-115">The default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="33e75-116">Akış uç ölçeklendirme hakkında daha fazla bilgi için bkz: [bu](media-services-portal-scale-streaming-endpoints.md) konu.</span><span class="sxs-lookup"><span data-stu-id="33e75-116">For information about how to scale the streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="33e75-117">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="33e75-117">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="33e75-118">Geliştirme ortamınızı kurun ve app.config dosyanızı [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md) bölümünde açıklandığı gibi bağlantı bilgileriyle doldurun.</span><span class="sxs-lookup"><span data-stu-id="33e75-118">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="add-code-that-manages-streaming-endpoints"></a><span data-ttu-id="33e75-119">Akış uç noktalarını yönetir kodu ekleyin</span><span class="sxs-lookup"><span data-stu-id="33e75-119">Add code that manages streaming endpoints</span></span>
    
<span data-ttu-id="33e75-120">Program.cs kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="33e75-120">Replace the code in the Program.cs with the following code:</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.Live;

    namespace AMSStreamingEndpoint
    {
        class Program
        {
        // Read values from the App.config file.
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


## <a name="next-steps"></a><span data-ttu-id="33e75-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="33e75-121">Next steps</span></span>
<span data-ttu-id="33e75-122">Media Services öğrenme yollarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="33e75-122">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="33e75-123">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="33e75-123">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

