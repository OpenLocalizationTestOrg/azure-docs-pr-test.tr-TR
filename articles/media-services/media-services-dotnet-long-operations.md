---
title: "uzun süre çalışan işlemleri aaaPolling | Microsoft Docs"
description: "Bu konuda gösterilmektedir nasıl toopoll uzun süre çalışan işlemleri."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 9a68c4b1-6159-42fe-9439-a3661a90ae03
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: f8315a5ddbe484d794c3e2164e47dd9e70521671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="delivering-live-streaming-with-azure-media-services"></a><span data-ttu-id="fb93e-103">Azure Media Services ile canlı akış teslim etme</span><span class="sxs-lookup"><span data-stu-id="fb93e-103">Delivering Live Streaming with Azure Media Services</span></span>

## <a name="overview"></a><span data-ttu-id="fb93e-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="fb93e-104">Overview</span></span>

<span data-ttu-id="fb93e-105">Microsoft Azure Media Services istekleri gönderme tooMedia Hizmetleri toostart işlemleri API'ler sunar (örneğin: oluşturma, başlatma, durdurma veya kanal silme).</span><span class="sxs-lookup"><span data-stu-id="fb93e-105">Microsoft Azure Media Services offers APIs that send requests tooMedia Services toostart operations (for example: create, start, stop, or delete a channel).</span></span> <span data-ttu-id="fb93e-106">Bu uzun süre çalışan işlemlerdir.</span><span class="sxs-lookup"><span data-stu-id="fb93e-106">These operations are long-running.</span></span>

<span data-ttu-id="fb93e-107">Merhaba Media Services .NET SDK'sı hello isteği göndermek ve hello işlemi toocomplete (dahili olarak, bazı aralıklarla yoklama API işlemi ilerlemesi hello) bekleyin API'ler sağlar.</span><span class="sxs-lookup"><span data-stu-id="fb93e-107">hello Media Services .NET SDK provides APIs that send hello request and wait for hello operation toocomplete (internally, hello APIs are polling for operation progress at some intervals).</span></span> <span data-ttu-id="fb93e-108">Örneğin, kanal çağırdığınızda. Merhaba kanal başlatıldıktan sonra Start(), hello yöntemi döndürür.</span><span class="sxs-lookup"><span data-stu-id="fb93e-108">For example, when you call channel.Start(), hello method returns after hello channel is started.</span></span> <span data-ttu-id="fb93e-109">Merhaba zaman uyumsuz sürümü de kullanabilirsiniz: kanal bekler. StartAsync() (görev tabanlı zaman uyumsuz desen hakkında daha fazla bilgi için bkz: [DOKUNUN](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span><span class="sxs-lookup"><span data-stu-id="fb93e-109">You can also use hello asynchronous version: await channel.StartAsync() (for information about Task-based Asynchronous Pattern, see [TAP](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span></span> <span data-ttu-id="fb93e-110">Bir operation isteğini göndermek ve hello işlemi tamamlanana kadar hello durumunun yoklaması API'leri "yoklama yöntemleri" adı verilir.</span><span class="sxs-lookup"><span data-stu-id="fb93e-110">APIs that send an operation request and then poll for hello status until hello operation is complete are called “polling methods”.</span></span> <span data-ttu-id="fb93e-111">Bu yöntemler (özellikle hello zaman uyumsuz sürümü) zengin istemci uygulamaları ve/veya durum bilgisi olan hizmetler için önerilir.</span><span class="sxs-lookup"><span data-stu-id="fb93e-111">These methods (especially hello Async version) are recommended for rich client applications and/or stateful services.</span></span>

<span data-ttu-id="fb93e-112">Burada bir uygulama uzun süre çalışan bir http isteği için Bekleyemez ve toopoll hello işlemi ilerleme durumu için el ile istediği senaryo vardır.</span><span class="sxs-lookup"><span data-stu-id="fb93e-112">There are scenarios where an application cannot wait for a long running http request and wants toopoll for hello operation progress manually.</span></span> <span data-ttu-id="fb93e-113">Tipik bir örnek durum bilgisiz web hizmetiyle etkileşim kurarken bir tarayıcı olabilir: hello tarayıcı istekleri toocreate bir kanal, hello web hizmeti uzun süren bir işlem başlatır ve işlem kimliği toohello tarayıcı hello döndürür.</span><span class="sxs-lookup"><span data-stu-id="fb93e-113">A typical example would be a browser interacting with a stateless web service: when hello browser requests toocreate a channel, hello web service initiates a long running operation and returns hello operation ID toohello browser.</span></span> <span data-ttu-id="fb93e-114">Merhaba tarayıcı sonra hello web hizmeti tooget hello işlem durumunu hello kimliğine göre isteyebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="fb93e-114">hello browser could then ask hello web service tooget hello operation status based on hello ID.</span></span> <span data-ttu-id="fb93e-115">Merhaba Media Services .NET SDK'sı, bu senaryo için yararlı olan API'ler sağlar.</span><span class="sxs-lookup"><span data-stu-id="fb93e-115">hello Media Services .NET SDK provides APIs that are useful for this scenario.</span></span> <span data-ttu-id="fb93e-116">Bu API'leri "yoklama olmayan yöntemleri" adı verilir.</span><span class="sxs-lookup"><span data-stu-id="fb93e-116">These APIs are called “non-polling methods”.</span></span>
<span data-ttu-id="fb93e-117">Merhaba "yoklama olmayan yöntemleri" sahip adlandırma modeli aşağıdaki hello: gönderme*OperationName*işlemi (örneğin, SendCreateOperation).</span><span class="sxs-lookup"><span data-stu-id="fb93e-117">hello “non-polling methods” have hello following naming pattern: Send*OperationName*Operation (for example, SendCreateOperation).</span></span> <span data-ttu-id="fb93e-118">Gönderme*OperationName*işlemi yöntemleri döndürür hello **IOperation** nesne; hello döndürülen nesne kullanılan tootrack hello işlemi olabilecek bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="fb93e-118">Send*OperationName*Operation methods return hello **IOperation** object; hello returned object contains information that can be used tootrack hello operation.</span></span> <span data-ttu-id="fb93e-119">Merhaba gönderme*OperationName*OperationAsync yöntemleri döndürür **görev<IOperation>**.</span><span class="sxs-lookup"><span data-stu-id="fb93e-119">hello Send*OperationName*OperationAsync methods return **Task<IOperation>**.</span></span>

<span data-ttu-id="fb93e-120">Şu anda sınıfları destek yoklama olmayan yöntemler aşağıdaki hello: **kanal**, **StreamingEndpoint**, ve **Program**.</span><span class="sxs-lookup"><span data-stu-id="fb93e-120">Currently, hello following classes support non-polling methods:  **Channel**, **StreamingEndpoint**, and **Program**.</span></span>

<span data-ttu-id="fb93e-121">Merhaba işlem durumunu, kullanım hello toopoll **GetOperation** hello yöntemi **OperationBaseCollection** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="fb93e-121">toopoll for hello operation status, use hello **GetOperation** method on hello **OperationBaseCollection** class.</span></span> <span data-ttu-id="fb93e-122">Aralıkları toocheck hello işlem durumunu izleyen hello kullan: için **kanal** ve **StreamingEndpoint** işlemleri, 30 saniye kullanın; **Program** işlemleri, 10 kullanın saniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="fb93e-122">Use hello following intervals toocheck hello operation status: for **Channel** and **StreamingEndpoint** operations, use 30 seconds; for **Program** operations, use 10 seconds.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="fb93e-123">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fb93e-123">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="fb93e-124">Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="fb93e-124">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span>

## <a name="example"></a><span data-ttu-id="fb93e-125">Örnek</span><span class="sxs-lookup"><span data-stu-id="fb93e-125">Example</span></span>

<span data-ttu-id="fb93e-126">Merhaba aşağıdaki örnek olarak adlandırılan bir sınıfı tanımlar **ChannelOperations**.</span><span class="sxs-lookup"><span data-stu-id="fb93e-126">hello following example defines a class called **ChannelOperations**.</span></span> <span data-ttu-id="fb93e-127">Bu sınıf tanımını web hizmet sınıf tanımı için bir başlangıç noktası olabilir.</span><span class="sxs-lookup"><span data-stu-id="fb93e-127">This class definition could be a starting point for your web service class definition.</span></span> <span data-ttu-id="fb93e-128">Kolaylık olması için hello aşağıdaki örneklerde hello async olmayan sürümleri yöntemlerden birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="fb93e-128">For simplicity, hello following examples use hello non-async versions of methods.</span></span>

<span data-ttu-id="fb93e-129">Hello örnek ayrıca bu sınıf hello istemci nasıl kullanabilir gösterir.</span><span class="sxs-lookup"><span data-stu-id="fb93e-129">hello example also shows how hello client might use this class.</span></span>

### <a name="channeloperations-class-definition"></a><span data-ttu-id="fb93e-130">ChannelOperations sınıf tanımı</span><span class="sxs-lookup"><span data-stu-id="fb93e-130">ChannelOperations class definition</span></span>

    using Microsoft.WindowsAzure.MediaServices.Client;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Net;

    /// <summary> 
    /// hello ChannelOperations class only implements 
    /// hello Channel’s creation operation. 
    /// </summary> 
    public class ChannelOperations
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        public ChannelOperations()
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
        }

        /// <summary>  
        /// Initiates hello creation of a new channel.  
        /// </summary>  
        /// <param name="channelName">Name toobe given toohello new channel</param>  
        /// <returns>  
        /// Operation Id for hello long running operation being executed by Media Services. 
        /// Use this operation Id toopoll for hello channel creation status. 
        /// </returns> 
        public string StartChannelCreation(string channelName)
        {
            var operation = _context.Channels.SendCreateOperation(
                new ChannelCreationOptions
                {
                    Name = channelName,
                    Input = CreateChannelInput(),
                    Preview = CreateChannelPreview(),
                    Output = CreateChannelOutput()
                });

            return operation.Id;
        }

        /// <summary> 
        /// Checks if hello operation has been completed. 
        /// If hello operation succeeded, hello created channel Id is returned in hello out parameter.
        /// </summary> 
        /// <param name="operationId">hello operation Id.</param> 
        /// <param name="channel">
        /// If hello operation succeeded, 
        /// hello created channel Id is returned in hello out parameter.</param>
        /// <returns>Returns false if hello operation is still in progress; otherwise, true.</returns> 
        public bool IsCompleted(string operationId, out string channelId)
        {
            IOperation operation = _context.Operations.GetOperation(operationId);
            bool completed = false;

            channelId = null;

            switch (operation.State)
            {
                case OperationState.Failed:
                    // Handle hello failure. 
                    // For example, throw an exception. 
                    // Use hello following information in hello exception: operationId, operation.ErrorMessage.
                    break;
                case OperationState.Succeeded:
                    completed = true;
                    channelId = operation.TargetEntityId;
                    break;
                case OperationState.InProgress:
                    completed = false;
                    break;
            }
            return completed;
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
                                Address = IPAddress.Parse("0.0.0.0"),
                                SubnetPrefixLength = 0
                            }
                        }
                }
            };
        }

        private static ChannelOutput CreateChannelOutput()
        {
            return new ChannelOutput
            {
                Hls = new ChannelOutputHls { FragmentsPerSegment = 1 }
            };
        }
    }

### <a name="hello-client-code"></a><span data-ttu-id="fb93e-131">Merhaba istemci kodu</span><span class="sxs-lookup"><span data-stu-id="fb93e-131">hello client code</span></span>
    ChannelOperations channelOperations = new ChannelOperations();
    string opId = channelOperations.StartChannelCreation("MyChannel001");

    string channelId = null;
    bool isCompleted = false;

    while (isCompleted == false)
    {
        System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
        isCompleted = channelOperations.IsCompleted(opId, out channelId);
    }

    // If we got here, we should have hello newly created channel id.
    Console.WriteLine(channelId);



## <a name="media-services-learning-paths"></a><span data-ttu-id="fb93e-132">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="fb93e-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fb93e-133">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="fb93e-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

