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
# <a name="use-azure-media-video-thumbnails-toocreate-a-video-summarization"></a>Azure medya Video küçük resimleri tooCreate bir Video özeti kullanın
## <a name="overview"></a>Genel Bakış
Merhaba **Azure medya Video küçük resimleri** medya işlemcisi (MP) toocreate toopreview uzun bir video Özeti yalnızca isteyen yararlı toocustomers olan video özetini sağlar. Örneğin, müşteriler toosee kısa "özeti video" isteyebilirsiniz küçük üzerine bunlar vurgulu zaman. Merhaba parametrelerinin uyguladıkça tarafından **Azure medya Video küçük resimleri** birleştirme teknolojisi tooalgorithmically açıklayıcı subclip oluşturmak ve yapılandırma hazır hello MP güçlü görüntüsü algılama kullanabilirsiniz.  

Merhaba **Azure medya Video küçük** MP şu anda önizlemede.

Bu konu hakkında ayrıntılar verir **Azure medya Video küçük** ve gösterir nasıl toouse .NET için Media Services SDK'sı ile.

## <a name="limitations"></a>Sınırlamalar

Videonuzu farklı perde, oluşan değil, bazı durumlarda, hello çıktı yalnızca tek bir görüntüsü.

## <a name="video-summary-example"></a>Video özeti örneği
Hangi hello Azure medya Video küçük resimleri medya işlemcisi yapabilirsiniz ilişkin bazı örnekler şunlardır:

### <a name="original-video"></a>Özgün video
[Özgün video](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Faed33834-ec2d-4788-88b5-a4505b3d032c%2FMicrosoft%27s%20HoloLens%20Live%20Demonstration.ism%2Fmanifest)

### <a name="video-thumbnail-result"></a>Video küçük resim sonucu
[Video küçük resim sonucu](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Ff5c91052-4232-41d4-b531-062e07b6a9ae%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="task-configuration-preset"></a>Görev yapılandırması (hazır)
Video küçük resim görev oluştururken **Azure medya Video küçük resimleri**, bir yapılandırma hazır belirtmeniz gerekir. küçük resim örnek yukarıda Hello temel JSON yapılandırma aşağıdaki hello ile oluşturuldu:

    {"version":"1.0"}

Şu anda şu parametreler hello değiştirebilirsiniz:

| Param | Açıklama |
| --- | --- |
| outputAudio |Merhaba sonuç video, ses içerip içermeyeceğini belirtir. <br/>İzin verilen değerler: True veya False. Varsayılan true'dur. |
| fadeInFadeOut |Belirtir desteklemediğini yavaşça geçişleri hello ayrı hareket küçük resimleri arasında kullanılır.  <br/>İzin verilen değerler: True veya False.  Varsayılan true'dur. |
| maxMotionThumbnailDurationInSecs |Ne kadar süreyle hello tüm sonuç video belirten Tamsayı olacaktır.  Varsayılan özgün video süresine bağlıdır. |

Merhaba aşağıdaki tabloda açıklanmaktadır hello varsayılan süre, ne zaman **maxMotionThumbnailInSecs** kullanılmaz.

|  |  |  |
| --- | --- | --- | --- | --- |
| Video süresi |d < 3 min |3 min < d < 15 dakika |
| Küçük resim süresi |15 saniye (2-3 planda) |30 saniye (3-5 planda) |

Merhaba aşağıdaki JSON kullanılabilir parametreleri ayarlar.

    {
        "version": "1.0",
        "options": {
            "outputAudio": "true",
            "maxMotionThumbnailDurationInSecs": "10",
            "fadeInFadeOut": "true"
        }
    }

## <a name="net-sample-code"></a>.NET örnek kod

Merhaba aşağıdaki program gösterir nasıl yapılır:

1. Bir varlık oluşturun ve hello varlığa bir medya dosyasını yükleyin.
2. Json hazır aşağıdaki hello içeren bir yapılandırma dosyasına dayalı bir video küçük resim görevini içeren bir işi oluşturur. 
   
        {                
            "version": "1.0",
            "options": {
                "outputAudio": "true",
                "maxMotionThumbnailDurationInSecs": "30",
                "fadeInFadeOut": "false"
            }
        }
3. Merhaba çıktı dosyaları indirir. 

#### <a name="create-and-configure-a-visual-studio-project"></a>Visual Studio projesi oluşturup yapılandırma

Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Örnek

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

### <a name="video-thumbnail-output"></a>Video küçük resim çıkışı
[Video küçük resim çıkışı](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Fd06f24dc-bc81-488e-a8d0-348b7dc41b56%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>İlgili bağlantılar
[Azure Media Services Analytics a genel bakış](media-services-analytics-overview.md)

[Azure medya analizi gösterileri](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

