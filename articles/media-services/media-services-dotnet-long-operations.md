---
title: "Uzun süre çalışan işlemleri yoklama | Microsoft Docs"
description: "Bu konu, uzun süre çalışan işlemleri yoklamak gösterilmektedir."
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
ms.openlocfilehash: 7123a2d44d3b7c332afe30fb0fcea88ca29e313a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="delivering-live-streaming-with-azure-media-services"></a><span data-ttu-id="fa295-103">Azure Media Services ile canlı akış teslim etme</span><span class="sxs-lookup"><span data-stu-id="fa295-103">Delivering Live Streaming with Azure Media Services</span></span>

## <a name="overview"></a><span data-ttu-id="fa295-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="fa295-104">Overview</span></span>

<span data-ttu-id="fa295-105">Microsoft Azure Media Services işlemleri başlatmak için Media Services istekleri göndermek API'ler sunar (örneğin: oluşturma, başlatma, durdurma veya kanal silme).</span><span class="sxs-lookup"><span data-stu-id="fa295-105">Microsoft Azure Media Services offers APIs that send requests to Media Services to start operations (for example: create, start, stop, or delete a channel).</span></span> <span data-ttu-id="fa295-106">Bu uzun süre çalışan işlemlerdir.</span><span class="sxs-lookup"><span data-stu-id="fa295-106">These operations are long-running.</span></span>

<span data-ttu-id="fa295-107">Media Services .NET SDK'sı işlemin tamamlanmasını bekleyin ve isteği Gönder API'ler sağlar (dahili olarak, API işlem ilerlemesi için bazı aralıklarla yoklama).</span><span class="sxs-lookup"><span data-stu-id="fa295-107">The Media Services .NET SDK provides APIs that send the request and wait for the operation to complete (internally, the APIs are polling for operation progress at some intervals).</span></span> <span data-ttu-id="fa295-108">Örneğin, kanal çağırdığınızda. Kanal başlatıldıktan sonra Start(), yöntemi döndürür.</span><span class="sxs-lookup"><span data-stu-id="fa295-108">For example, when you call channel.Start(), the method returns after the channel is started.</span></span> <span data-ttu-id="fa295-109">Zaman uyumsuz sürümü de kullanabilirsiniz: kanal bekler. StartAsync() (görev tabanlı zaman uyumsuz desen hakkında daha fazla bilgi için bkz: [DOKUNUN](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span><span class="sxs-lookup"><span data-stu-id="fa295-109">You can also use the asynchronous version: await channel.StartAsync() (for information about Task-based Asynchronous Pattern, see [TAP](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span></span> <span data-ttu-id="fa295-110">İşlem isteği gönderin ve işlemi tamamlanana kadar durumunun yoklaması API'leri "yoklama yöntemleri" adı verilir.</span><span class="sxs-lookup"><span data-stu-id="fa295-110">APIs that send an operation request and then poll for the status until the operation is complete are called “polling methods”.</span></span> <span data-ttu-id="fa295-111">Bu yöntemler (özellikle zaman uyumsuz sürümü) zengin istemci uygulamaları ve/veya durum bilgisi olan hizmetler için önerilir.</span><span class="sxs-lookup"><span data-stu-id="fa295-111">These methods (especially the Async version) are recommended for rich client applications and/or stateful services.</span></span>

<span data-ttu-id="fa295-112">Burada bir uygulama uzun süre çalışan bir http isteği için Bekleyemez ve işlem ilerlemesi için el ile yoklamaya istediği senaryo vardır.</span><span class="sxs-lookup"><span data-stu-id="fa295-112">There are scenarios where an application cannot wait for a long running http request and wants to poll for the operation progress manually.</span></span> <span data-ttu-id="fa295-113">Tipik bir örnek durum bilgisiz web hizmetiyle etkileşim kurarken bir tarayıcı olabilir: tarayıcı bir kanal oluşturmak isterse, web hizmeti uzun süren bir işlem başlatır ve işlem kimliği tarayıcıya döndürür.</span><span class="sxs-lookup"><span data-stu-id="fa295-113">A typical example would be a browser interacting with a stateless web service: when the browser requests to create a channel, the web service initiates a long running operation and returns the operation ID to the browser.</span></span> <span data-ttu-id="fa295-114">Tarayıcı sonra kimliğine göre işlem durumunu almak için web hizmeti isteyebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="fa295-114">The browser could then ask the web service to get the operation status based on the ID.</span></span> <span data-ttu-id="fa295-115">Media Services .NET SDK'sı, bu senaryo için yararlı olan API'ler sağlar.</span><span class="sxs-lookup"><span data-stu-id="fa295-115">The Media Services .NET SDK provides APIs that are useful for this scenario.</span></span> <span data-ttu-id="fa295-116">Bu API'leri "yoklama olmayan yöntemleri" adı verilir.</span><span class="sxs-lookup"><span data-stu-id="fa295-116">These APIs are called “non-polling methods”.</span></span>
<span data-ttu-id="fa295-117">Aşağıdaki adlandırma deseni "Yoklama olmayan yöntemler" sahiptir: gönderme*OperationName*işlemi (örneğin, SendCreateOperation).</span><span class="sxs-lookup"><span data-stu-id="fa295-117">The “non-polling methods” have the following naming pattern: Send*OperationName*Operation (for example, SendCreateOperation).</span></span> <span data-ttu-id="fa295-118">Gönderme*OperationName*işlemi yöntemleri döndürür **IOperation** nesne; döndürülen nesnesi işlemi izlemek için kullanılan bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="fa295-118">Send*OperationName*Operation methods return the **IOperation** object; the returned object contains information that can be used to track the operation.</span></span> <span data-ttu-id="fa295-119">Gönderme*OperationName*OperationAsync yöntemleri döndürür **görev<IOperation>**.</span><span class="sxs-lookup"><span data-stu-id="fa295-119">The Send*OperationName*OperationAsync methods return **Task<IOperation>**.</span></span>

<span data-ttu-id="fa295-120">Şu anda aşağıdaki sınıflar yoklama olmayan yöntemlerini destekler: **kanal**, **StreamingEndpoint**, ve **Program**.</span><span class="sxs-lookup"><span data-stu-id="fa295-120">Currently, the following classes support non-polling methods:  **Channel**, **StreamingEndpoint**, and **Program**.</span></span>

<span data-ttu-id="fa295-121">İçin işlem durumunu yoklamak için **GetOperation** yöntemi **OperationBaseCollection** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="fa295-121">To poll for the operation status, use the **GetOperation** method on the **OperationBaseCollection** class.</span></span> <span data-ttu-id="fa295-122">İşlem durumunu denetlemek için şu aralıklar kullanın: için **kanal** ve **StreamingEndpoint** işlemleri, 30 saniye kullanın; **Program** işlemleri, 10 saniye kullanın.</span><span class="sxs-lookup"><span data-stu-id="fa295-122">Use the following intervals to check the operation status: for **Channel** and **StreamingEndpoint** operations, use 30 seconds; for **Program** operations, use 10 seconds.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="fa295-123">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fa295-123">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="fa295-124">Geliştirme ortamınızı kurun ve app.config dosyanızı [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md) bölümünde açıklandığı gibi bağlantı bilgileriyle doldurun.</span><span class="sxs-lookup"><span data-stu-id="fa295-124">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span>

## <a name="example"></a><span data-ttu-id="fa295-125">Örnek</span><span class="sxs-lookup"><span data-stu-id="fa295-125">Example</span></span>

<span data-ttu-id="fa295-126">Aşağıdaki örnek adlı bir sınıf tanımlar **ChannelOperations**.</span><span class="sxs-lookup"><span data-stu-id="fa295-126">The following example defines a class called **ChannelOperations**.</span></span> <span data-ttu-id="fa295-127">Bu sınıf tanımını web hizmet sınıf tanımı için bir başlangıç noktası olabilir.</span><span class="sxs-lookup"><span data-stu-id="fa295-127">This class definition could be a starting point for your web service class definition.</span></span> <span data-ttu-id="fa295-128">Kolaylık olması için aşağıdaki örneklerde yöntemlerinin olmayan zaman uyumsuz sürümlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="fa295-128">For simplicity, the following examples use the non-async versions of methods.</span></span>

<span data-ttu-id="fa295-129">Örnek, ayrıca istemciyi bu sınıfın nasıl kullanabilir gösterir.</span><span class="sxs-lookup"><span data-stu-id="fa295-129">The example also shows how the client might use this class.</span></span>

### <a name="channeloperations-class-definition"></a><span data-ttu-id="fa295-130">ChannelOperations sınıf tanımı</span><span class="sxs-lookup"><span data-stu-id="fa295-130">ChannelOperations class definition</span></span>

    using Microsoft.WindowsAzure.MediaServices.Client;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Net;

    /// <summary> 
    /// The ChannelOperations class only implements 
    /// the Channel’s creation operation. 
    /// </summary> 
    public class ChannelOperations
    {
        // Read values from the App.config file.
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
        /// Initiates the creation of a new channel.  
        /// </summary>  
        /// <param name="channelName">Name to be given to the new channel</param>  
        /// <returns>  
        /// Operation Id for the long running operation being executed by Media Services. 
        /// Use this operation Id to poll for the channel creation status. 
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
        /// Checks if the operation has been completed. 
        /// If the operation succeeded, the created channel Id is returned in the out parameter.
        /// </summary> 
        /// <param name="operationId">The operation Id.</param> 
        /// <param name="channel">
        /// If the operation succeeded, 
        /// the created channel Id is returned in the out parameter.</param>
        /// <returns>Returns false if the operation is still in progress; otherwise, true.</returns> 
        public bool IsCompleted(string operationId, out string channelId)
        {
            IOperation operation = _context.Operations.GetOperation(operationId);
            bool completed = false;

            channelId = null;

            switch (operation.State)
            {
                case OperationState.Failed:
                    // Handle the failure. 
                    // For example, throw an exception. 
                    // Use the following information in the exception: operationId, operation.ErrorMessage.
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

### <a name="the-client-code"></a><span data-ttu-id="fa295-131">İstemci kodu</span><span class="sxs-lookup"><span data-stu-id="fa295-131">The client code</span></span>
    ChannelOperations channelOperations = new ChannelOperations();
    string opId = channelOperations.StartChannelCreation("MyChannel001");

    string channelId = null;
    bool isCompleted = false;

    while (isCompleted == false)
    {
        System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
        isCompleted = channelOperations.IsCompleted(opId, out channelId);
    }

    // If we got here, we should have the newly created channel id.
    Console.WriteLine(channelId);



## <a name="media-services-learning-paths"></a><span data-ttu-id="fa295-132">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="fa295-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fa295-133">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="fa295-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

