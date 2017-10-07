---
title: Azure medya Analizi ile aaaDetect hareketlerin | Microsoft Docs
description: "Merhaba, tooefficiently aksi uzun ve olaysız video içinde ilgi bölümleri tanımlamak Azure medya hareket algılayıcısı medya işlemci (MP) etkinleştirir."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: d144f813-1a55-442f-a895-5c4cb6d0aeae
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: milanga;juliako;
ms.openlocfilehash: cb431375c92222053ed2239dd4e45767524dab68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a>Azure medya Analizi ile hareketlerin Algıla
## <a name="overview"></a>Genel Bakış
Merhaba **Azure medya hareket algılayıcısı** , tooefficiently aksi uzun ve olaysız video içinde ilgi bölümleri tanımlamak medya işlemci (MP) etkinleştirir. Hareket algılama hareket oluştuğu statik kamera görüntülerinin tooidentify bölümlerini hello video üzerinde kullanılabilir. Zaman damgaları ve bölge hello olayın gerçekleştiği sınırlayıcı hello meta verileri içeren bir JSON dosyası oluşturur.

Doğru güvenlik video akışları hedeflenen, bu mümkün toocategorize hareket ilgili olayları ve hatalı pozitif sonuç gölgeleri ve aydınlatma değişiklikleri gibi teknolojisidir. Bu işlem, sonsuz ilgisiz olaylarıyla aşırı uzun gözetleme videolar gelen ilgi mümkün tooextract dakika devam ederken adresinize olmadan kamera akışları toogenerate güvenlik uyarıları sağlar.

Merhaba **Azure medya hareket algılayıcısı** MP şu anda önizlemede.

Bu konu hakkında ayrıntılar verir **Azure medya hareket algılayıcısı** ve gösterir nasıl toouse .NET için Media Services SDK'sı ile

## <a name="motion-detector-input-files"></a>Hareket algılayıcısı giriş dosyaları
Video dosyaları. Şu anda biçimleri aşağıdaki hello desteklenir: MP4, MOV ve WMV.

## <a name="task-configuration-preset"></a>Görev yapılandırması (hazır)
Bir görev oluştururken **Azure medya hareket algılayıcısı**, bir yapılandırma hazır belirtmeniz gerekir. 

### <a name="parameters"></a>Parametreler
Şu parametreler hello kullanabilirsiniz:

| Ad | Seçenekler | Açıklama | Varsayılan |
| --- | --- | --- | --- |
| sensitivityLevel |Dize: 'düşük', 'Orta', 'yüksek' |Hangi hareketlerin adresindeki bildirilir Hello hassasiyet düzeyini ayarlar. Bu hatalı pozitif sonuç tooadjust miktarını ayarlayın. |'Orta' |
| frameSamplingValue |Pozitif tamsayı |Merhaba sıklığı algoritması çalıştığı ayarlar. Her çerçeve eşittir 1, 2 her 2 çerçeve ve benzeri anlamına gelir. |1 |
| detectLightChange |Boolean: 'true', 'false' |Hafif değişiklikleri hello sonuçlarında bildirilen olup olmadığını belirler |'False' |
| mergeTimeThreshold |Xs zamanı: Ss: dd:<br/>Örnek: 00:00:03 |Burada 2 olayları birleştirilmiş ve olması 1 bildirilen hareket olaylar arasındaki Hello zaman penceresi belirtir. |00:00:00 |
| detectionZones |Algılama bölgeleri dizisi:<br/>-3 veya daha fazla noktalar dizisi algılama bölgedir<br/>-Noktasıdır x ve y 0 too1 gelen koordinat. |Çokgen algılama bölgeleri toobe kullanılan Hello listesi açıklar.<br/>Sonuçları hello ilk olma 'ID' ile bir kimliği olarak hello bölge ile bildirilir: 0 |Merhaba tüm çerçeve kapsayan tek bir bölge. |

### <a name="json-example"></a>JSON örneği
    {
      "version": "1.0",
      "options": {
        "sensitivityLevel": "medium",
        "frameSamplingValue": 1,
        "detectLightChange": "False",
        "mergeTimeThreshold":
        "00:00:02",
        "detectionZones": [
          [
            {"x": 0, "y": 0},
            {"x": 0.5, "y": 0},
            {"x": 0, "y": 1}
           ],
          [
            {"x": 0.3, "y": 0.3},
            {"x": 0.55, "y": 0.3},
            {"x": 0.8, "y": 0.3},
            {"x": 0.8, "y": 0.55},
            {"x": 0.8, "y": 0.8},
            {"x": 0.55, "y": 0.8},
            {"x": 0.3, "y": 0.8},
            {"x": 0.3, "y": 0.55}
          ]
        ]
      }
    }


## <a name="motion-detector-output-files"></a>Hareket algılayıcısı çıktı dosyaları
Hareket algılama işi hello hareket uyarılar ve bunların kategorilerde hello video tanımlayan hello çıkış varlık bir JSON dosyası döndürür. Merhaba dosyası başlangıç saatini ve süresini hello video algılanan hareket hakkında bilgi içerir.

bir sabit arka planda video (örn. bir izleme video) hareket nesneleri olduğunuzda hello hareket algılayıcısı API göstergeleri sağlar. Merhaba hareket algılayıcısı aydınlatma ve gölge değişiklikleri gibi eğitilen tooreduce yanlış alarmlar ' dir. Geçerli sınırlamalar hello algoritmalarının gece görme videoları, yarı saydam nesneleri ve küçük nesneleri içerir.

### <a id="output_elements"></a>Merhaba çıkış JSON dosyasının öğeleri
> [!NOTE]
> Merhaba en son sürümdeki hello çıkış JSON biçimi değişti ve bazı müşteriler için önemli bir değişiklik gösterebilir.
> 
> 

Merhaba aşağıdaki tabloda hello çıkış JSON dosyasının öğelerini açıklar.

| Öğesi | Açıklama |
| --- | --- |
| Sürüm |Bu toohello hello Video API sürümü ifade eder. Merhaba geçerli sürüm 2'dir. |
| Zaman Çizelgesi |"Hello videonun saniyede"çizgilerine. |
| Uzaklık |"çizgilerine" veritabanındaki tarih damgası Hello zaman uzaklığı. Video API'leri 1.0 sürümünde, bu her zaman 0 olacaktır. Gelecekte destekliyoruz senaryoları, bu değeri değiştirebilirsiniz. |
| Kare hızı |Saniyedeki kare sayısı hello video. |
| Genişlik, Yükseklik |Toohello genişliğini ve yüksekliğini piksel cinsinden görüntü hello başvuruyor. |
| Başlatma |Merhaba "çizgilerine" timestamp başlatın. |
| Süre |Merhaba olayda "çizgilerine" Merhaba uzunluğu. |
| aralığı |Her giriş hello olayda "çizgilerine" Merhaba aralığı. |
| Olaylar |Her olay parça bu süre içinde algılanan hello hareket içerir. |
| Tür |Merhaba geçerli sürümde, bu her zaman genel hareket ' 2' dir. Bu etiket Video API'leri hello esneklik toocategorize hareket gelecekteki sürümlerde de sağlar. |
| RegionID |Yukarıda açıklandığı şekilde, bu her zaman bu sürümde 0 olacaktır. Bu etiket Video API hello esneklik toofind hareket gelecekteki sürümlerinde çeşitli bölgelerdeki sağlar. |
| Bölgeler |Toohello alanında hareket hakkında burada verdiğiniz videonuzu başvuruyor. <br/><br/>-"id" Merhaba Bölge alanı temsil eder – Bu sürümde yalnızca bir olduğundan, kimliği 0. <br/>-"tür" Merhaba bölge önem verdiğiniz hareket hello şeklini temsil eder. Şu anda, "dikdörtgen" ve "Çokgen" desteklenir.<br/> "Dikdörtgen" belirtilmişse hello bölge boyutu X, vardır. Y, genişlik ve yükseklik. Merhaba X ve Y koordinatları hello üst sol XY koordinatları 0.0 too1.0 normalleştirilmiş ölçeğini hello bölgede temsil eder. Merhaba genişlik ve yükseklik 0.0 too1.0 normalleştirilmiş ölçeğini hello bölgede hello boyutunu temsil eder. Merhaba geçerli sürümde, X, Y, genişlik ve yükseklik her zaman giderilen 0, 0 ve 1, 1. <br/>"Çokgen" belirtilmişse, hello bölge boyutları noktalar vardır. <br/> |
| Parçaları |Merhaba meta verilerini yukarı parçaları olarak adlandırılan farklı kesimler halinde öbekli. Her parça başlangıç, süre, aralığı sayısı ve olay içerir. Hiçbir olay ile bir parça yok hareket bu başlangıç saatini ve süresini sırasında algılandı anlamına gelir. |
| Köşeli ayraçlar] |Her köşeli ayraç hello olay bir aralığa temsil eder. Boş köşeli ayraçlar hiçbir hareket anlamına bu aralık için algılandı. |
| Konumları |Bu yeni girişi olayları altında hello hareket oluştuğu hello konumunu listeler. Merhaba algılama bölgeleri daha fazla belirli budur. |

bir JSON çıktı örneği Hello aşağıda verilmiştir

    {
      "version": 2,
      "timescale": 23976,
      "offset": 0,
      "framerate": 24,
      "width": 1280,
      "height": 720,
      "regions": [
        {
          "id": 0,
          "type": "polygon",
          "points": [{'x': 0, 'y': 0},
            {'x': 0.5, 'y': 0},
            {'x': 0, 'y': 1}]
        }
      ],
      "fragments": [
        {
          "start": 0,
          "duration": 226765
        },
        {
          "start": 226765,
          "duration": 47952,
          "interval": 999,
          "events": [
            [
              {
                "type": 2,
                "typeName": "motion",
                "locations": [
                  {
                    "x": 0.004184,
                    "y": 0.007463,
                    "width": 0.991667,
                    "height": 0.985185
                  }
                ],
                "regionId": 0
              }
            ],

    …
## <a name="limitations"></a>Sınırlamalar
* desteklenen hello giriş video biçimleri MP4, MOV ve WMV içerir.
* Hareket algılama sabit arka plan videolar için optimize edilmiştir. Merhaba algoritması aydınlatma değişiklikleri ve gölgeleri gibi yanlış alarmlar azaltma odaklanır.
* Bazı hareket tootechnical zorluklar algılanamayabilir; Örneğin gece görme videoları, yarı saydam nesneler ve küçük nesneleri.

## <a name="net-sample-code"></a>.NET örnek kod

Merhaba aşağıdaki program gösterir nasıl yapılır:

1. Bir varlık oluşturun ve hello varlığa bir medya dosyasını yükleyin.
2. Json hazır aşağıdaki hello içeren bir yapılandırma dosyasına dayalı bir video hareket algılama görev ile bir iş oluşturun. 
   
        {
          "Version": "1.0",
          "Options": {
            "SensitivityLevel": "medium",
            "FrameSamplingValue": 1,
            "DetectLightChange": "False",
            "MergeTimeThreshold":
            "00:00:02",
            "DetectionZones": [
              [
                {"x": 0, "y": 0},
                {"x": 0.5, "y": 0},
                {"x": 0, "y": 1}
               ],
              [
                {"x": 0.3, "y": 0.3},
                {"x": 0.55, "y": 0.3},
                {"x": 0.8, "y": 0.3},
                {"x": 0.8, "y": 0.55},
                {"x": 0.8, "y": 0.8},
                {"x": 0.55, "y": 0.8},
                {"x": 0.3, "y": 0.8},
                {"x": 0.3, "y": 0.55}
              ]
            ]
          }
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

    namespace VideoMotionDetection
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

                // Run hello VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference tooAzure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

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
[Azure Media Services hareket algılayıcısı blogu](https://azure.microsoft.com/blog/motion-detector-update/)

[Azure Media Services Analytics a genel bakış](media-services-analytics-overview.md)

[Azure medya analizi gösterileri](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

