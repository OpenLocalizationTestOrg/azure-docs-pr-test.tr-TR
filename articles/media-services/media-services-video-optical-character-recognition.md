---
title: Azure medya analizi OCR aaaDigitize metinle | Microsoft Docs
description: "Azure medya analizi OCR (optik karakter tanıma) düzenlenebilir, aranabilir dijital metne video dosyalarında tooconvert metin içeriği sağlar.  Bu, medya video sinyali hello anlamlı meta verilerin tooautomate hello ayıklama sağlar."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 307c196e-3a50-4f4b-b982-51585448ffc6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 0476c3ba3942b2c5182a34a429909adbf5c75ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-analytics-tooconvert-text-content-in-video-files-into-digital-text"></a>Azure medya analizi tooconvert metin içeriği video dosyalarında dijital metne kullanın.
## <a name="overview"></a>Genel Bakış
Video dosyalarından tooextract metin içerik gerekir ve düzenlenebilir, aranabilir dijital metin oluşturan Azure medya analizi OCR (optik karakter tanıma) kullanmanız gerekir. Bu Azure medya işlemcisi video dosyalarında metin içeriği algılar ve kendi kullanımınız için metin dosyaları oluşturur. OCR, tooautomate hello ayıklama anlamlı meta verilerin hello video sinyali medyanızın sağlar.

Bir arama motoru ile birlikte kullanıldığında, kolayca medyanızı metin dizin ve içeriğinizi hello bulunabilirliğini artırmak. Bu bir video kaydı veya bir slayt gösterisi sunumu ekran yakalama gibi yüksek oranda metinsel videoda son derece yararlıdır. Hello Azure OCR medya işlemcisi dijital metin için optimize edilmiştir.

Merhaba **Azure medya OCR** medya işlemcisi şu anda önizlemede.

Bu konu hakkında ayrıntılar verir **Azure medya OCR** ve gösterir nasıl toouse .NET için Media Services SDK'sı ile. Ek bilgi ve örnekler için bkz: [bu blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).

## <a name="ocr-input-files"></a>OCR giriş dosyaları
Video dosyaları. Şu anda biçimleri aşağıdaki hello desteklenir: MP4, MOV ve WMV.

## <a name="task-configuration"></a>Görev yapılandırması
Görev yapılandırması (hazır). Bir görev oluştururken **Azure medya OCR**, JSON veya XML kullanarak önceden belirlenmiş bir yapılandırma belirtmeniz gerekir. 

>[!NOTE]
>Merhaba OCR altyapısı minimum 40 piksel toomaximum 32000 piksel görüntü bölgesiyle hem yükseklik/genişlik içinde geçerli bir giriş olarak yalnızca alır.
>

### <a name="attribute-descriptions"></a>Öznitelik tanımlarını
| Öznitelik adı | Açıklama |
| --- | --- |
|AdvancedOutput| Merhaba JSON çıktısını AdvancedOutput tootrue ayarlarsanız, her tek Word'de (toplama toophrases ve bölgeler) için konumsal veri içermez. Bu ayrıntılar toosee istemiyorsanız hello bayrağı toofalse ayarlayın. Merhaba varsayılan değer false şeklindedir. Daha fazla bilgi için bkz: [bu blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).|
| Dil |(isteğe bağlı) için hangi toolook metin hello dilini açıklar. Merhaba aşağıdakilerden biri: Otomatik Algıla (varsayılan), Arapça, ChineseSimplified, ChineseTraditional, Çekçe Danca, Felemenkçe, İngilizce, Fince, Fransızca, Almanca, Yunanca, Macarca, İtalyanca, Japonca, Korece, Norveççe, Lehçe, Portekizce, Rumence, Rusça, SerbianCyrillic, SerbianLatin, Slovakça, İspanyolca, İsveççe, Türkçe. |
| TextOrientation |(isteğe bağlı) için hangi toolook metnin hello yönünü açıklar.  Tüm harfler üstündeki hello "Sol" anlamına gelir hello sola doğru işaret.  Varsayılan metin (örneğin, kitaptaki bulunan) "Yedekleme" yönlendirilmiş çağrılabilir.  Merhaba aşağıdakilerden biri: Otomatik Algıla (varsayılan), sağ, aşağı, sol. |
| TimeInterval |(isteğe bağlı) hello örnekleme oranını açıklar.  1/2 saniyede varsayılandır.<br/>JSON biçimi – SS: dd:. SSS (varsayılan 00:00:00.500)<br/>XML biçiminde – W3C XSD süresi ilkel (varsayılan PT0.5) |
| DetectRegions |(isteğe bağlı) Hangi toodetect metinde hello video çerçevesinde bölgeler belirtme DetectRegion nesnelerinin bir dizisi.<br/>Bir DetectRegion nesnesi dört tamsayı değerleri aşağıdaki hello yapılır:<br/>Sol – hello sol kenar boşluğu piksellerden<br/>Üst – hello üst kenar boşluğu piksellerden<br/>Genişlik – hello bölge piksel cinsinden genişliği<br/>Yükseklik – hello bölge piksel cinsinden yüksekliği |

#### <a name="json-preset-example"></a>Örnek JSON hazır

    {
        "Version":1.0, 
        "Options": 
        {
            "AdvancedOutput":"true",
            "Language":"English", 
            "TimeInterval":"00:00:01.5",
            "TextOrientation":"Up",
            "DetectRegions": [
                    {
                       "Left": 10,
                       "Top": 10,
                       "Width": 100,
                       "Height": 50
                    }
             ]
        }
    }


#### <a name="xml-preset-example"></a>XML hazır örneği
    <?xml version=""1.0"" encoding=""utf-16""?>
    <VideoOcrPreset xmlns:xsi=""http://www.w3.org/2001/XMLSchema-instance"" xmlns:xsd=""http://www.w3.org/2001/XMLSchema"" Version=""1.0"" xmlns=""http://www.windowsazure.com/media/encoding/Preset/2014/03"">
      <Options>
         <AdvancedOutput>true</AdvancedOutput>
         <Language>English</Language>
         <TimeInterval>PT1.5S</TimeInterval>
         <DetectRegions>
             <DetectRegion>
                   <Left>10</Left>
                   <Top>10</Top>
                   <Width>100</Width>
                   <Height>50</Height>
            </DetectRegion>
       </DetectRegions>
       <TextOrientation>Up</TextOrientation>
      </Options>
    </VideoOcrPreset>

## <a name="ocr-output-files"></a>OCR çıktı dosyaları
Merhaba çıktı hello OCR medya işlemcisi bir JSON dosyasıdır.

### <a name="elements-of-hello-output-json-file"></a>Merhaba çıkış JSON dosyasının öğeleri
Merhaba Video OCR çıktı hello karakterler videonuzu içinde bulundu zaman kesimli veri sağlar.  Tam olarak çözümlenmesinde ilgilenen hello sözcükleri dil veya yönde toohone gibi öznitelikleri kullanabilirsiniz. 

Merhaba çıkış öznitelikleri aşağıdaki hello içerir:

| Öğesi | Açıklama |
| --- | --- |
| Zaman Çizelgesi |Merhaba videonun saniyede "çizgilerine" |
| Uzaklık |zaman damgaları için uzaklık. Video API'leri 1.0 sürümünde, bu her zaman 0 olacaktır. |
| Kare hızı |Saniyedeki kare hello video sayısı |
| Genişlik |Merhaba video piksel cinsinden genişliği |
| Yükseklik |Merhaba piksel cinsinden görüntü yüksekliği |
| Parçaları |hangi hello meta verileri öbekli video zamana dayalı parçalarını dizisi |
| start |Başlangıç saati "çizgilerine" parçadaki |
| Süre |"çizgilerine" parçadaki uzunluğu |
| interval |Parça verilen hello içinde her olayın aralığı |
| etkinlikler |bölgeleri içeren bir dizi |
| Bölge |nesnesini temsil eden kelimeler ve ifadeler algılandı |
| Dil |bir bölge içinde algılanan hello metin dili |
| Yönlendirme |bir bölge içinde algılanan hello metnin yönünü |
| satırları |bir bölge içinde algılanan metin satırı dizisi |
| Metin |Merhaba gerçek metin |

### <a name="json-output-example"></a>JSON çıkış örneği
Merhaba aşağıdaki çıktı örneği hello genel video bilgi ve birkaç video parçalarını içerir. Video her parçasında OCR MP hello dili ve onun metin hizalamasını tarafından algılanan her bölge içerir. Merhaba bölge ayrıca her word satır hello hattın metin, hello satırın konumunu ve bu satırdaki her bir word bilgileri (word içerik, konum ve güvenilirlik) ile bu bölgede yer alır. Merhaba aşağıda bir örnek verilmiştir ve bazı açıklamalar satır içi yerleştirin.

    {
        "version": 1, 
        "timescale": 90000, 
        "offset": 0, 
        "framerate": 30, 
        "width": 640, 
        "height": 480,  // general video information
        "fragments": [
            {
                "start": 0, 
                "duration": 180000, 
                "interval": 90000,  // hello time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // hello detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including hello text and hello position
                                    {
                                        "text": "One Two", 
                                        "left": 10, 
                                        "top": 10, 
                                        "right": 210, 
                                        "bottom": 110, 
                                        "word": [  // word information array in this line
                                            {
                                                "text": "One", 
                                                "left": 10, 
                                                "top": 10, 
                                                "right": 110, 
                                                "bottom": 110, 
                                                "confidence": 900
                                            }, 
                                            {
                                                "text": "Two", 
                                                "left": 110, 
                                                "top": 10, 
                                                "right": 210, 
                                                "bottom": 110, 
                                                "confidence": 910
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                ]
            }
        ]
    }

## <a name="net-sample-code"></a>.NET örnek kod

Merhaba aşağıdaki program gösterir nasıl yapılır:

1. Bir varlık oluşturun ve hello varlığa bir medya dosyasını yükleyin.
2. İşi bir OCR yapılandırma/hazır dosyası oluşturun.
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

    namespace OCR
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

                // Run hello OCR job.
                var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                            @"C:\supportFiles\OCR\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
            }

            static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My OCR Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My OCR Job");

                // Get a reference tooAzure Media OCR.
                string MediaProcessorName = "Azure Media OCR";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My OCR Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);

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

