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
# <a name="delivering-live-streaming-with-azure-media-services"></a>Azure Media Services ile canlı akış teslim etme

## <a name="overview"></a>Genel Bakış

Microsoft Azure Media Services istekleri gönderme tooMedia Hizmetleri toostart işlemleri API'ler sunar (örneğin: oluşturma, başlatma, durdurma veya kanal silme). Bu uzun süre çalışan işlemlerdir.

Merhaba Media Services .NET SDK'sı hello isteği göndermek ve hello işlemi toocomplete (dahili olarak, bazı aralıklarla yoklama API işlemi ilerlemesi hello) bekleyin API'ler sağlar. Örneğin, kanal çağırdığınızda. Merhaba kanal başlatıldıktan sonra Start(), hello yöntemi döndürür. Merhaba zaman uyumsuz sürümü de kullanabilirsiniz: kanal bekler. StartAsync() (görev tabanlı zaman uyumsuz desen hakkında daha fazla bilgi için bkz: [DOKUNUN](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)). Bir operation isteğini göndermek ve hello işlemi tamamlanana kadar hello durumunun yoklaması API'leri "yoklama yöntemleri" adı verilir. Bu yöntemler (özellikle hello zaman uyumsuz sürümü) zengin istemci uygulamaları ve/veya durum bilgisi olan hizmetler için önerilir.

Burada bir uygulama uzun süre çalışan bir http isteği için Bekleyemez ve toopoll hello işlemi ilerleme durumu için el ile istediği senaryo vardır. Tipik bir örnek durum bilgisiz web hizmetiyle etkileşim kurarken bir tarayıcı olabilir: hello tarayıcı istekleri toocreate bir kanal, hello web hizmeti uzun süren bir işlem başlatır ve işlem kimliği toohello tarayıcı hello döndürür. Merhaba tarayıcı sonra hello web hizmeti tooget hello işlem durumunu hello kimliğine göre isteyebilirsiniz Merhaba Media Services .NET SDK'sı, bu senaryo için yararlı olan API'ler sağlar. Bu API'leri "yoklama olmayan yöntemleri" adı verilir.
Merhaba "yoklama olmayan yöntemleri" sahip adlandırma modeli aşağıdaki hello: gönderme*OperationName*işlemi (örneğin, SendCreateOperation). Gönderme*OperationName*işlemi yöntemleri döndürür hello **IOperation** nesne; hello döndürülen nesne kullanılan tootrack hello işlemi olabilecek bilgiler içerir. Merhaba gönderme*OperationName*OperationAsync yöntemleri döndürür **görev<IOperation>**.

Şu anda sınıfları destek yoklama olmayan yöntemler aşağıdaki hello: **kanal**, **StreamingEndpoint**, ve **Program**.

Merhaba işlem durumunu, kullanım hello toopoll **GetOperation** hello yöntemi **OperationBaseCollection** sınıfı. Aralıkları toocheck hello işlem durumunu izleyen hello kullan: için **kanal** ve **StreamingEndpoint** işlemleri, 30 saniye kullanın; **Program** işlemleri, 10 kullanın saniye sayısı.

## <a name="create-and-configure-a-visual-studio-project"></a>Visual Studio projesi oluşturup yapılandırma

Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md).

## <a name="example"></a>Örnek

Merhaba aşağıdaki örnek olarak adlandırılan bir sınıfı tanımlar **ChannelOperations**. Bu sınıf tanımını web hizmet sınıf tanımı için bir başlangıç noktası olabilir. Kolaylık olması için hello aşağıdaki örneklerde hello async olmayan sürümleri yöntemlerden birini kullanın.

Hello örnek ayrıca bu sınıf hello istemci nasıl kullanabilir gösterir.

### <a name="channeloperations-class-definition"></a>ChannelOperations sınıf tanımı

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

### <a name="hello-client-code"></a>Merhaba istemci kodu
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



## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

