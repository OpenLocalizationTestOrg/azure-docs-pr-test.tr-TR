---
title: "Medya Kodlayıcısı standart hazır özelleştirme | Microsoft Docs"
description: "Bu konu, Medya Kodlayıcısı standart görev hazır özelleştirerek gelişmiş kodlama gerçekleştirmek gösterilmiştir. Konu, Media Services .NET SDK'sı bir kodlama görevi ve proje oluşturmak için nasıl kullanılacağını gösterir. Ayrıca, kodlama işi özel hazır ayarları sağlamak nasıl gösterir."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec95392f-d34a-4c22-a6df-5274eaac445b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: b4d25f07349043da8cb745930fde3371c98f9960
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="customizing-media-encoder-standard-presets"></a><span data-ttu-id="9b121-105">Özelleştirme Medya Kodlayıcısı standart hazır ayarları</span><span class="sxs-lookup"><span data-stu-id="9b121-105">Customizing Media Encoder Standard presets</span></span>

## <a name="overview"></a><span data-ttu-id="9b121-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="9b121-106">Overview</span></span>

<span data-ttu-id="9b121-107">Bu konu, bir özel hazır kullanarak Medya Kodlayıcısı standart (MES ile) gelişmiş kodlama gerçekleştirmek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="9b121-107">This topic shows how to perform advanced encoding with Media Encoder Standard (MES) using a custom preset.</span></span> <span data-ttu-id="9b121-108">Konu .NET kodlama görev ve bu görevi yürüten bir iş oluşturmak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="9b121-108">The topic uses .NET to create an encoding task and a job that executes this task.</span></span>  

<span data-ttu-id="9b121-109">Bu konuda bir hazır gerçekleştirerek özelleştirmek nasıl göreceksiniz [H264 Çoklu bit hızı 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) önceden ve katman sayısını azaltır.</span><span class="sxs-lookup"><span data-stu-id="9b121-109">In this topic you will see how to customize a preset by taking the [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) preset and reducing the number of layers.</span></span> <span data-ttu-id="9b121-110">[Medya Kodlayıcısı standart özelleştirme hazır ayarları](media-services-advanced-encoding-with-mes.md) konu gelişmiş kodlama görevleri gerçekleştirmek için kullanılan özel hazır gösterir.</span><span class="sxs-lookup"><span data-stu-id="9b121-110">The [Customizing Media Encoder Standard presets](media-services-advanced-encoding-with-mes.md) topic demonstrates custom presets that can be used to perform advanced encoding tasks.</span></span>

## <span data-ttu-id="9b121-111"><a id="customizing_presets"></a>MES hazır özelleştirme</span><span class="sxs-lookup"><span data-stu-id="9b121-111"><a id="customizing_presets"></a> Customizing a MES preset</span></span>

### <a name="original-preset"></a><span data-ttu-id="9b121-112">Özgün hazır</span><span class="sxs-lookup"><span data-stu-id="9b121-112">Original preset</span></span>

<span data-ttu-id="9b121-113">Tanımlanan JSON Kaydet [H264 Çoklu bit hızı 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) .json uzantılı bazı dosyasındaki konu.</span><span class="sxs-lookup"><span data-stu-id="9b121-113">Save the JSON defined in the [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) topic in some file with .json extension.</span></span> <span data-ttu-id="9b121-114">Örneğin, **CustomPreset_JSON.json**.</span><span class="sxs-lookup"><span data-stu-id="9b121-114">For example, **CustomPreset_JSON.json**.</span></span>

### <a name="customized-preset"></a><span data-ttu-id="9b121-115">Özelleştirilmiş hazır</span><span class="sxs-lookup"><span data-stu-id="9b121-115">Customized preset</span></span>

<span data-ttu-id="9b121-116">Açık **CustomPreset_JSON.json** dosya ve ilk üç katmanlardan kaldırma **H264Layers** dosyanız aşağıdaki gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="9b121-116">Open the **CustomPreset_JSON.json** file and remove first three layers from **H264Layers** so your file looks like this.</span></span>

    
    {  
      "Version": 1.0,  
      "Codecs": [  
        {  
          "KeyFrameInterval": "00:00:02",  
          "H264Layers": [  
            {  
              "Profile": "Auto",  
              "Level": "auto",  
              "Bitrate": 1000,  
              "MaxBitrate": 1000,  
              "BufferWindow": "00:00:05",  
              "Width": 640,  
              "Height": 360,  
              "BFrames": 3,  
              "ReferenceFrames": 3,  
              "AdaptiveBFrame": true,  
              "Type": "H264Layer",  
              "FrameRate": "0/1"  
            },  
            {  
              "Profile": "Auto",  
              "Level": "auto",  
              "Bitrate": 650,  
              "MaxBitrate": 650,  
              "BufferWindow": "00:00:05",  
              "Width": 640,  
              "Height": 360,  
              "BFrames": 3,  
              "ReferenceFrames": 3,  
              "AdaptiveBFrame": true,  
              "Type": "H264Layer",  
              "FrameRate": "0/1"  
            },  
            {  
              "Profile": "Auto",  
              "Level": "auto",  
              "Bitrate": 400,  
              "MaxBitrate": 400,  
              "BufferWindow": "00:00:05",  
              "Width": 320,  
              "Height": 180,  
              "BFrames": 3,  
              "ReferenceFrames": 3,  
              "AdaptiveBFrame": true,  
              "Type": "H264Layer",  
              "FrameRate": "0/1"  
            }  
          ],  
          "Type": "H264Video"  
        },  
        {  
          "Profile": "AACLC",  
          "Channels": 2,  
          "SamplingRate": 48000,  
          "Bitrate": 128,  
          "Type": "AACAudio"  
        }  
      ],  
      "Outputs": [  
        {  
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",  
          "Format": {  
            "Type": "MP4Format"  
          }  
        }  
      ]  
    }  
    

## <span data-ttu-id="9b121-117"><a id="encoding_with_dotnet"></a>Media Services .NET SDK'sı ile kodlama</span><span class="sxs-lookup"><span data-stu-id="9b121-117"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="9b121-118">Aşağıdaki kod örneği, aşağıdaki görevleri gerçekleştirmek için Media Services .NET SDK'sını kullanır:</span><span class="sxs-lookup"><span data-stu-id="9b121-118">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

- <span data-ttu-id="9b121-119">Bir kodlama işi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9b121-119">Create an encoding job.</span></span>
- <span data-ttu-id="9b121-120">Medya Kodlayıcısı standart Kodlayıcı başvuru alın.</span><span class="sxs-lookup"><span data-stu-id="9b121-120">Get a reference to the Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="9b121-121">Önceki bölümde oluşturduğunuz özel JSON hazır yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9b121-121">Load the custom JSON preset that you created in the previous section.</span></span> 
  
        // Load the JSON from the local file.
        string configuration = File.ReadAllText(fileName);  

- <span data-ttu-id="9b121-122">Bir kodlama görev projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9b121-122">Add an encoding task to the job.</span></span> 
- <span data-ttu-id="9b121-123">Kodlanacak giriş varlık belirtin.</span><span class="sxs-lookup"><span data-stu-id="9b121-123">Specify the input asset to be encoded.</span></span>
- <span data-ttu-id="9b121-124">Kodlanmış varlık içerecek bir çıkış varlığı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9b121-124">Create an output asset that will contain the encoded asset.</span></span>
- <span data-ttu-id="9b121-125">İş ilerleme durumunu denetlemek için olay işleyici ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9b121-125">Add an event handler to check the job progress.</span></span>
- <span data-ttu-id="9b121-126">İşi göndermek.</span><span class="sxs-lookup"><span data-stu-id="9b121-126">Submit the job.</span></span>
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="9b121-127">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9b121-127">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="9b121-128">Geliştirme ortamınızı kurun ve app.config dosyanızı [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md) bölümünde açıklandığı gibi bağlantı bilgileriyle doldurun.</span><span class="sxs-lookup"><span data-stu-id="9b121-128">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="9b121-129">Örnek</span><span class="sxs-lookup"><span data-stu-id="9b121-129">Example</span></span>   

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace CustomizeMESPresests
    {
        class Program
        {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

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

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate the output using custom presets.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Load the XML (or JSON) from the local file.
            string configuration = File.ReadAllText("CustomPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        private static void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);
            switch (e.CurrentState)
            {
            case JobState.Finished:
                Console.WriteLine();
                Console.WriteLine("Job is finished. Please wait while local tasks or downloads complete...");
                break;
            case JobState.Canceling:
            case JobState.Queued:
            case JobState.Scheduled:
            case JobState.Processing:
                Console.WriteLine("Please wait...\n");
                break;
            case JobState.Canceled:
            case JobState.Error:

                // Cast sender as a job.
                IJob job = (IJob)sender;

                // Display or log error details as needed.
                break;
            default:
                break;
            }
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
            ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }

        }
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="9b121-130">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="9b121-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9b121-131">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="9b121-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="9b121-132">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9b121-132">See Also</span></span>
[<span data-ttu-id="9b121-133">Media Services kodlama a genel bakış</span><span class="sxs-lookup"><span data-stu-id="9b121-133">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

