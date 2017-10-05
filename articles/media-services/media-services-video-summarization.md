---
title: "Video özetleme oluşturmak için Azure medya Video küçük resimleri kullanın | Microsoft Docs"
description: "Video özetleme otomatik olarak kaynak video ilginç parçacıkları'i seçerek uzun videoları özetlerini oluşturmanıza yardımcı olabilir. Bu, uzun bir video beklenmesi gerekenler hızlı bir bakış sağlamak istediğinizde yararlıdır."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: a245529f-3150-4afc-93ec-e40d8a6b761d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: 5d5afdaf22ffea8f3b77a154acb5d0a8dda74405
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-media-video-thumbnails-to-create-a-video-summarization"></a><span data-ttu-id="c4c63-104">Video özetleme oluşturmak için Azure medya Video küçük resimleri kullanın</span><span class="sxs-lookup"><span data-stu-id="c4c63-104">Use Azure Media Video Thumbnails to Create a Video Summarization</span></span>
## <a name="overview"></a><span data-ttu-id="c4c63-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="c4c63-105">Overview</span></span>
<span data-ttu-id="c4c63-106">**Azure medya Video küçük resimleri** medya işlemcisi (MP), uzun bir video özetini Önizleme istediğiniz müşteriler için kullanışlı bir video özetini oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="c4c63-106">The **Azure Media Video Thumbnails** media processor (MP) enables you to create a summary of a video that is useful to customers who just want to preview a summary of a long video.</span></span> <span data-ttu-id="c4c63-107">Örneğin, müşteriler kısa bir "özeti video" görmek isteyebilirsiniz küçük üzerine bunlar vurgulu zaman.</span><span class="sxs-lookup"><span data-stu-id="c4c63-107">For example, customers might want to see a short "summary video" when they hover over a thumbnail.</span></span> <span data-ttu-id="c4c63-108">Parametreleri uyguladıkça tarafından **Azure medya Video küçük resimleri** yapılandırma hazır MP'nin güçlü görüntüsü algılama ve birleştirme teknolojisi algorithmically açıklayıcı subclip oluşturmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4c63-108">By tweaking the parameters of **Azure Media Video Thumbnails** through a configuration preset, you can use the MP's powerful shot detection and concatenation technology to algorithmically generate a descriptive subclip.</span></span>  

<span data-ttu-id="c4c63-109">**Azure medya Video küçük** MP şu anda önizlemede.</span><span class="sxs-lookup"><span data-stu-id="c4c63-109">The **Azure Media Video Thumbnail** MP is currently in Preview.</span></span>

<span data-ttu-id="c4c63-110">Bu konu hakkında ayrıntılar verir **Azure medya Video küçük** ve Media Services SDK'sı ile .NET için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="c4c63-110">This topic gives details about  **Azure Media Video Thumbnail** and shows how to use it with Media Services SDK for .NET.</span></span>

## <a name="limitations"></a><span data-ttu-id="c4c63-111">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="c4c63-111">Limitations</span></span>

<span data-ttu-id="c4c63-112">Videonuzu farklı perde, oluşan değil, bazı durumlarda, çıktı yalnızca tek bir görüntüsü.</span><span class="sxs-lookup"><span data-stu-id="c4c63-112">In some cases, if your video is not comprised of different scenes, the output will only be a single shot.</span></span>

## <a name="video-summary-example"></a><span data-ttu-id="c4c63-113">Video özeti örneği</span><span class="sxs-lookup"><span data-stu-id="c4c63-113">Video summary example</span></span>
<span data-ttu-id="c4c63-114">Azure medya Video küçük resimleri medya işlemcisi yapabileceklerine ilişkin bazı örnekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c4c63-114">Here are some examples of what the Azure Media Video Thumbnails media processor can do:</span></span>

### <a name="original-video"></a><span data-ttu-id="c4c63-115">Özgün video</span><span class="sxs-lookup"><span data-stu-id="c4c63-115">Original video</span></span>
[<span data-ttu-id="c4c63-116">Özgün video</span><span class="sxs-lookup"><span data-stu-id="c4c63-116">Original video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Faed33834-ec2d-4788-88b5-a4505b3d032c%2FMicrosoft%27s%20HoloLens%20Live%20Demonstration.ism%2Fmanifest)

### <a name="video-thumbnail-result"></a><span data-ttu-id="c4c63-117">Video küçük resim sonucu</span><span class="sxs-lookup"><span data-stu-id="c4c63-117">Video thumbnail result</span></span>
[<span data-ttu-id="c4c63-118">Video küçük resim sonucu</span><span class="sxs-lookup"><span data-stu-id="c4c63-118">Video thumbnail result</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Ff5c91052-4232-41d4-b531-062e07b6a9ae%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="task-configuration-preset"></a><span data-ttu-id="c4c63-119">Görev yapılandırması (hazır)</span><span class="sxs-lookup"><span data-stu-id="c4c63-119">Task configuration (preset)</span></span>
<span data-ttu-id="c4c63-120">Video küçük resim görev oluştururken **Azure medya Video küçük resimleri**, bir yapılandırma hazır belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4c63-120">When creating a video thumbnail task with **Azure Media Video Thumbnails**, you must specify a configuration preset.</span></span> <span data-ttu-id="c4c63-121">Yukarıdaki küçük örnek aşağıdaki temel JSON yapılandırma ile oluşturuldu:</span><span class="sxs-lookup"><span data-stu-id="c4c63-121">The above thumbnail sample was created with the following basic JSON configuration:</span></span>

    {"version":"1.0"}

<span data-ttu-id="c4c63-122">Şu anda, aşağıdaki parametreleri değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c4c63-122">Currently, you can change the following parameters:</span></span>

| <span data-ttu-id="c4c63-123">Param</span><span class="sxs-lookup"><span data-stu-id="c4c63-123">Param</span></span> | <span data-ttu-id="c4c63-124">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c4c63-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c4c63-125">outputAudio</span><span class="sxs-lookup"><span data-stu-id="c4c63-125">outputAudio</span></span> |<span data-ttu-id="c4c63-126">Sonuç video, ses içerip içermeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="c4c63-126">Specifies whether or not the resultant video contains any audio.</span></span> <br/><span data-ttu-id="c4c63-127">İzin verilen değerler: True veya False.</span><span class="sxs-lookup"><span data-stu-id="c4c63-127">Allowed values are: True or False.</span></span> <span data-ttu-id="c4c63-128">Varsayılan true'dur.</span><span class="sxs-lookup"><span data-stu-id="c4c63-128">Default is True.</span></span> |
| <span data-ttu-id="c4c63-129">fadeInFadeOut</span><span class="sxs-lookup"><span data-stu-id="c4c63-129">fadeInFadeOut</span></span> |<span data-ttu-id="c4c63-130">Belirtir desteklemediğini yavaşça geçişleri ayrı hareket küçük resimleri arasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c4c63-130">Specifies whether or not fade transitions are used between the separate motion thumbnails.</span></span>  <br/><span data-ttu-id="c4c63-131">İzin verilen değerler: True veya False.</span><span class="sxs-lookup"><span data-stu-id="c4c63-131">Allowed values are: True or False.</span></span>  <span data-ttu-id="c4c63-132">Varsayılan true'dur.</span><span class="sxs-lookup"><span data-stu-id="c4c63-132">Default is True.</span></span> |
| <span data-ttu-id="c4c63-133">maxMotionThumbnailDurationInSecs</span><span class="sxs-lookup"><span data-stu-id="c4c63-133">maxMotionThumbnailDurationInSecs</span></span> |<span data-ttu-id="c4c63-134">Tüm sonuç video ne kadar süreyle olmayacağını belirten tamsayı.</span><span class="sxs-lookup"><span data-stu-id="c4c63-134">Integer that specifies how long the entire resultant video shall be.</span></span>  <span data-ttu-id="c4c63-135">Varsayılan özgün video süresine bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="c4c63-135">Default depends on original video duration.</span></span> |

<span data-ttu-id="c4c63-136">Varsayılan süre aşağıdaki tabloda açıklanmaktadır, ne zaman **maxMotionThumbnailInSecs** kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="c4c63-136">The following table describes the default duration, when **maxMotionThumbnailInSecs** is not used.</span></span>

|  |  |  |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="c4c63-137">Video süresi</span><span class="sxs-lookup"><span data-stu-id="c4c63-137">Video duration</span></span> |<span data-ttu-id="c4c63-138">d < 3 min</span><span class="sxs-lookup"><span data-stu-id="c4c63-138">d < 3 min</span></span> |<span data-ttu-id="c4c63-139">3 min < d < 15 dakika</span><span class="sxs-lookup"><span data-stu-id="c4c63-139">3 min < d < 15 min</span></span> |
| <span data-ttu-id="c4c63-140">Küçük resim süresi</span><span class="sxs-lookup"><span data-stu-id="c4c63-140">Thumbnail duration</span></span> |<span data-ttu-id="c4c63-141">15 saniye (2-3 planda)</span><span class="sxs-lookup"><span data-stu-id="c4c63-141">15 sec (2-3 scenes)</span></span> |<span data-ttu-id="c4c63-142">30 saniye (3-5 planda)</span><span class="sxs-lookup"><span data-stu-id="c4c63-142">30 sec (3-5 scenes)</span></span> |

<span data-ttu-id="c4c63-143">Aşağıdaki JSON kullanılabilir parametreleri ayarlar.</span><span class="sxs-lookup"><span data-stu-id="c4c63-143">The following JSON sets available parameters.</span></span>

    {
        "version": "1.0",
        "options": {
            "outputAudio": "true",
            "maxMotionThumbnailDurationInSecs": "10",
            "fadeInFadeOut": "true"
        }
    }

## <a name="net-sample-code"></a><span data-ttu-id="c4c63-144">.NET örnek kod</span><span class="sxs-lookup"><span data-stu-id="c4c63-144">.NET sample code</span></span>

<span data-ttu-id="c4c63-145">Aşağıdaki program gösterir nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="c4c63-145">The following program shows how to:</span></span>

1. <span data-ttu-id="c4c63-146">Bir varlık oluşturun ve varlığa bir medya dosyasını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c4c63-146">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="c4c63-147">Aşağıdaki json hazır içeren bir yapılandırma dosyasına dayalı bir video küçük resim görevini içeren bir işi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c4c63-147">Creates a job with a video thumbnail task based on a configuration file that contains the following json preset.</span></span> 
   
        {                
            "version": "1.0",
            "options": {
                "outputAudio": "true",
                "maxMotionThumbnailDurationInSecs": "30",
                "fadeInFadeOut": "false"
            }
        }
3. <span data-ttu-id="c4c63-148">Çıkış dosyaları indirir.</span><span class="sxs-lookup"><span data-stu-id="c4c63-148">Downloads the output files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="c4c63-149">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c4c63-149">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="c4c63-150">Geliştirme ortamınızı kurun ve app.config dosyanızı [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md) bölümünde açıklandığı gibi bağlantı bilgileriyle doldurun.</span><span class="sxs-lookup"><span data-stu-id="c4c63-150">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="c4c63-151">Örnek</span><span class="sxs-lookup"><span data-stu-id="c4c63-151">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace VideoSummarization
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

            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);


                // Run the thumbnail job.
                var asset = RunVideoThumbnailJob(@"C:\supportFiles\VideoThumbnail\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoThumbnail\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoThumbnail\Output");
            }

            static IAsset RunVideoThumbnailJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Thumbnail Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Thumbnail Job");

                // Get a reference to Azure Media Video Thumbnails.
                string MediaProcessorName = "Azure Media Video Thumbnails";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Thumbnail Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My Video Thumbnail Output Asset", AssetCreationOptions.None);

                // Use the following event handler to check job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch the job.
                job.Submit();

                // Check job execution and wait for job to finish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, the event handling
                // method for job progress should log errors.  Here we check
                // for error state and exit if needed.
                if (job.State == JobState.Error)
                {
                    ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                    Console.WriteLine(string.Format("Error: {0}. {1}",
                                                    error.Code,
                                                    error.Message));
                    return null;
                }

                return job.OutputMediaAssets[0];
            }

            static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
            {
                IAsset asset = _context.Assets.Create(assetName, options);

                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                assetFile.Upload(filePath);

                return asset;
            }

            static void DownloadAsset(IAsset asset, string outputDirectory)
            {
                foreach (IAssetFile file in asset.AssetFiles)
                {
                    file.Download(Path.Combine(outputDirectory, file.Name));
                }
            }

            static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
            {
                var processor = _context.MediaProcessors
                    .Where(p => p.Name == mediaProcessorName)
                    .ToList()
                    .OrderBy(p => new Version(p.Version))
                    .LastOrDefault();

                if (processor == null)
                    throw new ArgumentException(string.Format("Unknown media processor",
                                                               mediaProcessorName));

                return processor;
            }

            static private void StateChanged(object sender, JobStateChangedEventArgs e)
            {
                Console.WriteLine("Job state changed event:");
                Console.WriteLine("  Previous state: " + e.PreviousState);
                Console.WriteLine("  Current state: " + e.CurrentState);

                switch (e.CurrentState)
                {
                    case JobState.Finished:
                        Console.WriteLine();
                        Console.WriteLine("Job is finished.");
                        Console.WriteLine();
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
                        // LogJobStop(job.Id);
                        break;
                    default:
                        break;
                }
            }

        }
    }

### <a name="video-thumbnail-output"></a><span data-ttu-id="c4c63-152">Video küçük resim çıkışı</span><span class="sxs-lookup"><span data-stu-id="c4c63-152">Video thumbnail output</span></span>
[<span data-ttu-id="c4c63-153">Video küçük resim çıkışı</span><span class="sxs-lookup"><span data-stu-id="c4c63-153">Video thumbnail output</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Fd06f24dc-bc81-488e-a8d0-348b7dc41b56%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="media-services-learning-paths"></a><span data-ttu-id="c4c63-154">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="c4c63-154">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c4c63-155">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="c4c63-155">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="c4c63-156">İlgili bağlantılar</span><span class="sxs-lookup"><span data-stu-id="c4c63-156">Related links</span></span>
[<span data-ttu-id="c4c63-157">Azure Media Services Analytics a genel bakış</span><span class="sxs-lookup"><span data-stu-id="c4c63-157">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="c4c63-158">Azure medya analizi gösterileri</span><span class="sxs-lookup"><span data-stu-id="c4c63-158">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

