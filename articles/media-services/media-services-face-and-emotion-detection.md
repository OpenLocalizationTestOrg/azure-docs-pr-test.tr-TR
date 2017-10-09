---
title: "aaaDetect yüz ve duygu Azure medya Analizi ile | Microsoft Docs"
description: "Bu konuda nasıl toodetect bakarken ve duygular Azure medya Analizi ile gösterilir."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5ca4692c-23f1-451d-9d82-cbc8bf0fd707
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: f58d81d82dde08a694cdb4d92c6bab6a40a9c157
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="detect-face-and-emotion-with-azure-media-analytics"></a>Yüz ve duygu Azure medya Analizi ile Algıla
## <a name="overview"></a>Genel Bakış
Merhaba **Azure medya yüz algılayıcısı** medya işlemcisi (MP) etkinleştirir, size, toocount, izleme hareketleri ve hatta ölçer İzleyici katılım ve tepki yüz ifadeleri aracılığıyla. Bu hizmet, iki özellik içerir: 

* **Yüz algılama**
  
    Yüz algılama bulur ve video içinde İnsan yüzeyleri izler. Birden çok yüzeyleri algılanabilir ve bunların geçici bir JSON dosyası döndürülen hello zaman ve yer meta verilerle taşırken sonradan izlenmesi. İzleme sırasında toogive obstructed veya kısaca hello çerçeve bırakın olsa bile hello kişi ekranında dolaşma sırada aynı yönde tutarlı bir kimliği toohello dener.
  
  > [!NOTE]
  > Bu hizmet, yüz tanıma gerçekleştirmez. Merhaba çerçeve ayrıldığında ya da için obstructed hale bir kişi döndürmeleri zaman uzun yeni bir kimlik verilir.
  > 
  > 
* **Duygu algılama**
  
    Duygu algılama hello analiz mutluluk, sadness, Korku, öfke ve daha fazlası da dahil olmak üzere algılandı, hello yüzeyleri birden çok kendini özniteliklerinde döndürür yüz algılama medya işlemcisi isteğe bağlı bir bileşenidir. 

Merhaba **Azure medya yüz algılayıcısı** MP şu anda önizlemede.

Bu konu hakkında ayrıntılar verir **Azure medya yüz algılayıcısı** ve gösterir nasıl toouse .NET için Media Services SDK'sı ile.

## <a name="face-detector-input-files"></a>Yüz algılayıcısı giriş dosyaları
Video dosyaları. Şu anda biçimleri aşağıdaki hello desteklenir: MP4, MOV ve WMV.

## <a name="face-detector-output-files"></a>Yüz algılayıcısı çıktı dosyaları
Merhaba yüz algılama ve İzleme API, Yüksek duyarlılık yüz konumu algılama ve bir video too64 İnsan Yüz Yukarı algılayabilir izleme sağlar. Tamamen çıplak yüzeyleri yan yüz ve küçük yazıtipleri hello en iyi sonuçlar sağlayın (değerinden büyük veya eşit too24x24 piksel) olarak doğru olmayabilir.

Merhaba algılanan ve izlenen yüzeyleri döndürülür (sol, üst, genişlik ve yükseklik) koordinatlarıyla yüz kimliği numara belirten bir yanı sıra hello yüzeyleri piksel cinsinden hello görüntüdeki konumunu belirten, tek tek izlenmesini hello. Merhaba tamamen çıplak yüz kaybolduğunda veya hello çerçevede çakışan yüz kimliği koşullarda yatkın tooreset birden çok kimliği atanan bazı kişiler kaynaklanan numaralarıdır.

## <a id="output_elements"></a>Merhaba çıkış JSON dosyasının öğeleri

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

Yüz algılayıcısı (çok büyük alma durumunda burada hello olayları ayrılır) (burada zamana dayalı yığınlar halinde hello meta verileri bölünmüştür ve yalnızca ihtiyacınız yükleyebilirsiniz) parçalanma ve kesimlere ayırma teknikleri kullanır. Bazı basit hesaplamalar hello veri dönüştürme yardımcı olabilir. Örneğin, bir olay 2997 (çizgilerine/sn) bir ölçeğini 6300 (çizgilerine) başlatılan ve kare 29.97 (Çerçeve/sn), ardından hızına:

* Başlat/ölçeği = 2.1 saniye
* X frameRate saniye 63 çerçeveler =

## <a name="face-detection-input-and-output-example"></a>Algılama giriş yüz ve örnek çıkış
### <a name="input-video"></a>Giriş video
[Video girişi](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a>Görev yapılandırması (hazır)
Bir görev oluştururken **Azure medya yüz algılayıcısı**, bir yapılandırma hazır belirtmeniz gerekir. Yapılandırma hazır aşağıdaki hello yalnızca yüz algılama için ' dir.

    {
      "version":"1.0",
      "options":{
          "TrackingMode": "Fast"
      }
    }

#### <a name="attribute-descriptions"></a>Öznitelik tanımlarını
| Öznitelik adı | Açıklama |
| --- | --- |
| Modu |Hızlı - hızı, ancak daha az doğru (varsayılan) hızlı işleniyor.|

### <a name="json-output"></a>JSON çıktısını
Aşağıdaki örnek JSON çıktısını hello kesildi.

    {
    "version": 1,
    "timescale": 30000,
    "offset": 0,
    "framerate": 29.97,
    "width": 1280,
    "height": 720,
    "fragments": [
        {
        "start": 0,
        "duration": 60060
        },
        {
        "start": 60060,
        "duration": 60060,
        "interval": 1001,
        "events": [
            [
            {
                "id": 0,
                "x": 0.519531,
                "y": 0.180556,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517969,
                "y": 0.181944,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517187,
                "y": 0.183333,
                "width": 0.0851562,
                "height": 0.151389
            }
            ],

        . . . 

## <a name="emotion-detection-input-and-output-example"></a>Giriş ve çıkış duygu algılama örneği
### <a name="input-video"></a>Giriş video
[Video girişi](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a>Görev yapılandırması (hazır)
Bir görev oluştururken **Azure medya yüz algılayıcısı**, bir yapılandırma hazır belirtmeniz gerekir. Merhaba yapılandırma hazır aşağıdaki JSON tabanlı hello duygu algılama üzerinde toocreate belirtir.

    {
      "version": "1.0",
      "options": {
        "aggregateEmotionWindowMs": "987",
        "mode": "aggregateEmotion",
        "aggregateEmotionIntervalMs": "342"
      }
    }


#### <a name="attribute-descriptions"></a>Öznitelik tanımlarını
| Öznitelik adı | Açıklama |
| --- | --- |
| Modu |Yazıtipleri: Yalnızca algılama karşılaşıyor.<br/>PerFaceEmotion: her yüz algılama için ayrı ayrı duygu döndür.<br/>AggregateEmotion: Tüm yüzeyleri çerçevesinde dönüş ortalama duygu değerleri. |
| AggregateEmotionWindowMs |AggregateEmotion modunu seçtiyseniz kullanın. Merhaba video kullanılan tooproduce her bir toplama sonucu milisaniye cinsinden belirtir. |
| AggregateEmotionIntervalMs |AggregateEmotion modunu seçtiyseniz kullanın. Hangi sıklığı tooproduce toplama sonuçları ile belirtir. |

#### <a name="aggregate-defaults"></a>Birleşik Varsayılanları
Aşağıdaki değerler hello toplama penceresi ve aralığı ayarları için önerilir. AggregateEmotionWindowMs AggregateEmotionIntervalMs uzun olmalıdır.

|| Varsayılanları (s) | Min(s) | Max(s) |
|--- | --- | --- | --- |
| AggregateEmotionWindowMs |0.5 |2 |0.25|
| AggregateEmotionIntervalMs |0.5 |1 |0.25|

### <a name="json-output"></a>JSON çıktısını
JSON (kesilmiş) toplama duygu tanıma için çıktı:

    {
     "version": 1,
     "timescale": 30000,
     "offset": 0,
     "framerate": 29.97,
     "width": 1280,
     "height": 720,
     "fragments": [
       {
         "start": 0,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ]
         ]
       },
       {
         "start": 60060,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0.688541,
                 "happiness": 0.0586323,
                 "surprise": 0.227184,
                 "sadness": 0.00945675,
                 "anger": 0.00592107,
                 "disgust": 0.00154993,
                 "fear": 0.00450447,
                 "contempt": 0.0042109
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,

## <a name="limitations"></a>Sınırlamalar
* desteklenen hello giriş video biçimleri MP4, MOV ve WMV içerir.
* Merhaba algılanabilir yüz boyutu aralığı 24 x 24 too2048x2048 pikseldir. Bu aralık dışında Hello yüzeyleri algılanmaz.
* Her video için hello en fazla döndürülen yüzeyleri 64 sayısıdır.
* Bazı yüzeyleri tootechnical zorluklar algılanamayabilir; Örneğin çok büyük yüz açısı (poz head) ve büyük kapanması. Tamamen çıplak ve tamamen yakın yüzler hello en iyi sonuçlar sahip.

## <a name="net-sample-code"></a>.NET örnek kod

Merhaba aşağıdaki program gösterir nasıl yapılır:

1. Bir varlık oluşturun ve hello varlığa bir medya dosyasını yükleyin.
2. Json hazır aşağıdaki hello içeren bir yapılandırma dosyasına dayalı yüz algılama görevle ilgili bir iş oluşturun. 
   
        {
            "version": "1.0"
        }
3. Merhaba çıkış JSON dosyalarını indirin. 

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

    namespace FaceDetection
    {
        class Program
        {
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

                // Run hello FaceDetection job.
                var asset = RunFaceDetectionJob(@"C:\supportFiles\FaceDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\FaceDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\FaceDetection\Output");
            }

            static IAsset RunFaceDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Face Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Face Detection Job");

                // Get a reference tooAzure Media Face Detector.
                string MediaProcessorName = "Azure Media Face Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Face Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Face Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>İlgili bağlantılar
[Azure Media Services Analytics a genel bakış](media-services-analytics-overview.md)

[Azure medya analizi gösterileri](http://amslabs.azurewebsites.net/demos/Analytics.html)

