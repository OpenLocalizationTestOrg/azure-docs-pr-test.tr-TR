---
title: "aaaUse Azure medya Video küçük resimleri tooCreate bir Video özeti | Microsoft Docs"
description: "Video özetleme otomatik olarak hello kaynak video ilginç parçacıkları'i seçerek uzun videoları özetlerini oluşturmanıza yardımcı olabilir. Tooprovide hangi tooexpect uzun videoda hızlı bir genel bakış istediğinizde kullanışlıdır."
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
ms.openlocfilehash: 0a8f0bba6c12a948b940114fe4937e675688a8c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-video-thumbnails-toocreate-a-video-summarization"></a><span data-ttu-id="05bdf-104">Azure medya Video küçük resimleri tooCreate bir Video özeti kullanın</span><span class="sxs-lookup"><span data-stu-id="05bdf-104">Use Azure Media Video Thumbnails tooCreate a Video Summarization</span></span>
## <a name="overview"></a><span data-ttu-id="05bdf-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="05bdf-105">Overview</span></span>
<span data-ttu-id="05bdf-106">Merhaba **Azure medya Video küçük resimleri** medya işlemcisi (MP) toocreate toopreview uzun bir video Özeti yalnızca isteyen yararlı toocustomers olan video özetini sağlar.</span><span class="sxs-lookup"><span data-stu-id="05bdf-106">hello **Azure Media Video Thumbnails** media processor (MP) enables you toocreate a summary of a video that is useful toocustomers who just want toopreview a summary of a long video.</span></span> <span data-ttu-id="05bdf-107">Örneğin, müşteriler toosee kısa "özeti video" isteyebilirsiniz küçük üzerine bunlar vurgulu zaman.</span><span class="sxs-lookup"><span data-stu-id="05bdf-107">For example, customers might want toosee a short "summary video" when they hover over a thumbnail.</span></span> <span data-ttu-id="05bdf-108">Merhaba parametrelerinin uyguladıkça tarafından **Azure medya Video küçük resimleri** birleştirme teknolojisi tooalgorithmically açıklayıcı subclip oluşturmak ve yapılandırma hazır hello MP güçlü görüntüsü algılama kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05bdf-108">By tweaking hello parameters of **Azure Media Video Thumbnails** through a configuration preset, you can use hello MP's powerful shot detection and concatenation technology tooalgorithmically generate a descriptive subclip.</span></span>  

<span data-ttu-id="05bdf-109">Merhaba **Azure medya Video küçük** MP şu anda önizlemede.</span><span class="sxs-lookup"><span data-stu-id="05bdf-109">hello **Azure Media Video Thumbnail** MP is currently in Preview.</span></span>

<span data-ttu-id="05bdf-110">Bu konu hakkında ayrıntılar verir **Azure medya Video küçük** ve gösterir nasıl toouse .NET için Media Services SDK'sı ile.</span><span class="sxs-lookup"><span data-stu-id="05bdf-110">This topic gives details about  **Azure Media Video Thumbnail** and shows how toouse it with Media Services SDK for .NET.</span></span>

## <a name="limitations"></a><span data-ttu-id="05bdf-111">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="05bdf-111">Limitations</span></span>

<span data-ttu-id="05bdf-112">Videonuzu farklı perde, oluşan değil, bazı durumlarda, hello çıktı yalnızca tek bir görüntüsü.</span><span class="sxs-lookup"><span data-stu-id="05bdf-112">In some cases, if your video is not comprised of different scenes, hello output will only be a single shot.</span></span>

## <a name="video-summary-example"></a><span data-ttu-id="05bdf-113">Video özeti örneği</span><span class="sxs-lookup"><span data-stu-id="05bdf-113">Video summary example</span></span>
<span data-ttu-id="05bdf-114">Hangi hello Azure medya Video küçük resimleri medya işlemcisi yapabilirsiniz ilişkin bazı örnekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="05bdf-114">Here are some examples of what hello Azure Media Video Thumbnails media processor can do:</span></span>

### <a name="original-video"></a><span data-ttu-id="05bdf-115">Özgün video</span><span class="sxs-lookup"><span data-stu-id="05bdf-115">Original video</span></span>
[<span data-ttu-id="05bdf-116">Özgün video</span><span class="sxs-lookup"><span data-stu-id="05bdf-116">Original video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Faed33834-ec2d-4788-88b5-a4505b3d032c%2FMicrosoft%27s%20HoloLens%20Live%20Demonstration.ism%2Fmanifest)

### <a name="video-thumbnail-result"></a><span data-ttu-id="05bdf-117">Video küçük resim sonucu</span><span class="sxs-lookup"><span data-stu-id="05bdf-117">Video thumbnail result</span></span>
[<span data-ttu-id="05bdf-118">Video küçük resim sonucu</span><span class="sxs-lookup"><span data-stu-id="05bdf-118">Video thumbnail result</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Ff5c91052-4232-41d4-b531-062e07b6a9ae%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="task-configuration-preset"></a><span data-ttu-id="05bdf-119">Görev yapılandırması (hazır)</span><span class="sxs-lookup"><span data-stu-id="05bdf-119">Task configuration (preset)</span></span>
<span data-ttu-id="05bdf-120">Video küçük resim görev oluştururken **Azure medya Video küçük resimleri**, bir yapılandırma hazır belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="05bdf-120">When creating a video thumbnail task with **Azure Media Video Thumbnails**, you must specify a configuration preset.</span></span> <span data-ttu-id="05bdf-121">küçük resim örnek yukarıda Hello temel JSON yapılandırma aşağıdaki hello ile oluşturuldu:</span><span class="sxs-lookup"><span data-stu-id="05bdf-121">hello above thumbnail sample was created with hello following basic JSON configuration:</span></span>

    {"version":"1.0"}

<span data-ttu-id="05bdf-122">Şu anda şu parametreler hello değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="05bdf-122">Currently, you can change hello following parameters:</span></span>

| <span data-ttu-id="05bdf-123">Param</span><span class="sxs-lookup"><span data-stu-id="05bdf-123">Param</span></span> | <span data-ttu-id="05bdf-124">Açıklama</span><span class="sxs-lookup"><span data-stu-id="05bdf-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="05bdf-125">outputAudio</span><span class="sxs-lookup"><span data-stu-id="05bdf-125">outputAudio</span></span> |<span data-ttu-id="05bdf-126">Merhaba sonuç video, ses içerip içermeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="05bdf-126">Specifies whether or not hello resultant video contains any audio.</span></span> <br/><span data-ttu-id="05bdf-127">İzin verilen değerler: True veya False.</span><span class="sxs-lookup"><span data-stu-id="05bdf-127">Allowed values are: True or False.</span></span> <span data-ttu-id="05bdf-128">Varsayılan true'dur.</span><span class="sxs-lookup"><span data-stu-id="05bdf-128">Default is True.</span></span> |
| <span data-ttu-id="05bdf-129">fadeInFadeOut</span><span class="sxs-lookup"><span data-stu-id="05bdf-129">fadeInFadeOut</span></span> |<span data-ttu-id="05bdf-130">Belirtir desteklemediğini yavaşça geçişleri hello ayrı hareket küçük resimleri arasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="05bdf-130">Specifies whether or not fade transitions are used between hello separate motion thumbnails.</span></span>  <br/><span data-ttu-id="05bdf-131">İzin verilen değerler: True veya False.</span><span class="sxs-lookup"><span data-stu-id="05bdf-131">Allowed values are: True or False.</span></span>  <span data-ttu-id="05bdf-132">Varsayılan true'dur.</span><span class="sxs-lookup"><span data-stu-id="05bdf-132">Default is True.</span></span> |
| <span data-ttu-id="05bdf-133">maxMotionThumbnailDurationInSecs</span><span class="sxs-lookup"><span data-stu-id="05bdf-133">maxMotionThumbnailDurationInSecs</span></span> |<span data-ttu-id="05bdf-134">Ne kadar süreyle hello tüm sonuç video belirten Tamsayı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="05bdf-134">Integer that specifies how long hello entire resultant video shall be.</span></span>  <span data-ttu-id="05bdf-135">Varsayılan özgün video süresine bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="05bdf-135">Default depends on original video duration.</span></span> |

<span data-ttu-id="05bdf-136">Merhaba aşağıdaki tabloda açıklanmaktadır hello varsayılan süre, ne zaman **maxMotionThumbnailInSecs** kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="05bdf-136">hello following table describes hello default duration, when **maxMotionThumbnailInSecs** is not used.</span></span>

|  |  |  |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="05bdf-137">Video süresi</span><span class="sxs-lookup"><span data-stu-id="05bdf-137">Video duration</span></span> |<span data-ttu-id="05bdf-138">d < 3 min</span><span class="sxs-lookup"><span data-stu-id="05bdf-138">d < 3 min</span></span> |<span data-ttu-id="05bdf-139">3 min < d < 15 dakika</span><span class="sxs-lookup"><span data-stu-id="05bdf-139">3 min < d < 15 min</span></span> |
| <span data-ttu-id="05bdf-140">Küçük resim süresi</span><span class="sxs-lookup"><span data-stu-id="05bdf-140">Thumbnail duration</span></span> |<span data-ttu-id="05bdf-141">15 saniye (2-3 planda)</span><span class="sxs-lookup"><span data-stu-id="05bdf-141">15 sec (2-3 scenes)</span></span> |<span data-ttu-id="05bdf-142">30 saniye (3-5 planda)</span><span class="sxs-lookup"><span data-stu-id="05bdf-142">30 sec (3-5 scenes)</span></span> |

<span data-ttu-id="05bdf-143">Merhaba aşağıdaki JSON kullanılabilir parametreleri ayarlar.</span><span class="sxs-lookup"><span data-stu-id="05bdf-143">hello following JSON sets available parameters.</span></span>

    {
        "version": "1.0",
        "options": {
            "outputAudio": "true",
            "maxMotionThumbnailDurationInSecs": "10",
            "fadeInFadeOut": "true"
        }
    }

## <a name="net-sample-code"></a><span data-ttu-id="05bdf-144">.NET örnek kod</span><span class="sxs-lookup"><span data-stu-id="05bdf-144">.NET sample code</span></span>

<span data-ttu-id="05bdf-145">Merhaba aşağıdaki program gösterir nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="05bdf-145">hello following program shows how to:</span></span>

1. <span data-ttu-id="05bdf-146">Bir varlık oluşturun ve hello varlığa bir medya dosyasını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="05bdf-146">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="05bdf-147">Json hazır aşağıdaki hello içeren bir yapılandırma dosyasına dayalı bir video küçük resim görevini içeren bir işi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="05bdf-147">Creates a job with a video thumbnail task based on a configuration file that contains hello following json preset.</span></span> 
   
        {                
            "version": "1.0",
            "options": {
                "outputAudio": "true",
                "maxMotionThumbnailDurationInSecs": "30",
                "fadeInFadeOut": "false"
            }
        }
3. <span data-ttu-id="05bdf-148">Merhaba çıktı dosyaları indirir.</span><span class="sxs-lookup"><span data-stu-id="05bdf-148">Downloads hello output files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="05bdf-149">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="05bdf-149">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="05bdf-150">Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="05bdf-150">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="05bdf-151">Örnek</span><span class="sxs-lookup"><span data-stu-id="05bdf-151">Example</span></span>

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
            // Read values from hello App.config file.
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


                // Run hello thumbnail job.
                var asset = RunVideoThumbnailJob(@"C:\supportFiles\VideoThumbnail\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoThumbnail\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoThumbnail\Output");
            }

            static IAsset RunVideoThumbnailJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Thumbnail Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Thumbnail Job");

                // Get a reference tooAzure Media Video Thumbnails.
                string MediaProcessorName = "Azure Media Video Thumbnails";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Thumbnail Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Thumbnail Output Asset", AssetCreationOptions.None);

                // Use hello following event handler toocheck job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch hello job.
                job.Submit();

                // Check job execution and wait for job toofinish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, hello event handling
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

### <a name="video-thumbnail-output"></a><span data-ttu-id="05bdf-152">Video küçük resim çıkışı</span><span class="sxs-lookup"><span data-stu-id="05bdf-152">Video thumbnail output</span></span>
[<span data-ttu-id="05bdf-153">Video küçük resim çıkışı</span><span class="sxs-lookup"><span data-stu-id="05bdf-153">Video thumbnail output</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Fd06f24dc-bc81-488e-a8d0-348b7dc41b56%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="media-services-learning-paths"></a><span data-ttu-id="05bdf-154">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="05bdf-154">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="05bdf-155">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="05bdf-155">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="05bdf-156">İlgili bağlantılar</span><span class="sxs-lookup"><span data-stu-id="05bdf-156">Related links</span></span>
[<span data-ttu-id="05bdf-157">Azure Media Services Analytics a genel bakış</span><span class="sxs-lookup"><span data-stu-id="05bdf-157">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="05bdf-158">Azure medya analizi gösterileri</span><span class="sxs-lookup"><span data-stu-id="05bdf-158">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

