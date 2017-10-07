---
title: "Azure medya Analizi ile aaaRedact yüzeyleri | Microsoft Docs"
description: "Bu konuda, nasıl Azure medya Analizi ile tooredact bakarken gösterilir."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5b6d8b8c-5f4d-4fef-b3d6-dc22c6b5a0f5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;
ms.openlocfilehash: 1f5688a8c6374151c526a9c702b904d8c3e46164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a>Azure medya Analizi ile yüzeyleri Redaksiyon
## <a name="overview"></a>Genel Bakış
**Azure Media Redactor** olan bir [Azure medya analizi](media-services-analytics-overview.md) medya işlemcisi (MP) ölçeklenebilir yüz Redaksiyon hello bulutta sunar. Yüz Redaksiyon sipariş tooblur yüzeyleri seçilen kişilerin, video, toomodify sağlar. Toouse hello yüz Redaksiyon hizmeti ortak güvenliği ve haber medya senaryolarda isteyebilirsiniz. Saat tooredact el ile birden çok yüzeyleri içeren çekimi birkaç dakika sürebilir, ancak bu hizmet hello yüz ile birkaç basit adımla Redaksiyon işlem gerektirir. Daha fazla bilgi için bkz: [bu](https://azure.microsoft.com/blog/azure-media-redactor/) blogu.

Bu konu hakkında ayrıntılar verir **Azure medya Redactor** ve gösterir nasıl toouse .NET için Media Services SDK'sı ile.

Merhaba **Azure medya Redactor** MP şu anda önizlemede. Tüm ortak Azure bölgeleri yanı sıra ABD devlet kurumları ve Çin veri merkezleri kullanılabilir. Bu önizleme şu anda ücretsizdir. 

## <a name="face-redaction-modes"></a>Yüz Redaksiyon modları
Böylece Hello aynı tek diğer açıları bulanık her çerçevesinde video yüz algılama ve hello yüz izleme tarafından yüz Redaksiyon works her ikisi de iletir ve geriye doğru zaman içindeki nesne. Merhaba otomatik Redaksiyon işlemi çok karmaşık olduğu ve her zaman % 100'istenen çıkış, bu nedenle medya analizi, çeşitli şekillerde toomodify hello son çıktı sağlar üretmez.

Toplama tooa tamamen otomatik modda hello Seçimi/Kaldır-selection kimlikleri listesini aracılığıyla bulunan yazıtipleri, sağlayan iki geçişi iş akışı yok. Ayrıca, toomake çerçeve ayarlamalar hello MP rastgele JSON biçiminde bir meta veri dosyası kullanır. Bu iş akışı bölündüğünü **Çözümle** ve **Redact** modları. Her iki görevi bir işe çalıştıran tek bir geçiş iki modda hello birleştirebilirsiniz. Bu mod adlı **birleştirilmiş**.

### <a name="combined-mode"></a>Birleşik modu
Bu Redaksiyonu yapılmış bir mp4 otomatik olarak giriş herhangi bir el ile oluşturur.

| Aşama | Dosya adı | Notlar |
| --- | --- | --- |
| Giriş varlık |foo.bar |Video WMV, MOV veya MP4 biçimindeki |
| Giriş yapılandırma |İş yapılandırması hazır |{'version':'1.0 ', 'Seçenekler': {'modu': 'birleştirilmiş'}} |
| Çıkış varlık |foo_redacted.mp4 |Uygulanan Bulanıklaştırma ile video |

#### <a name="input-example"></a>Giriş örnek:
[Bu videoyu izleyin](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a>Çıkış örneği:
[Bu videoyu izleyin](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a>Mod Çözümle
Merhaba **analiz** geçişi hello iki geçişi iş akışının bir video girdi alır ve yüz konumların bir JSON dosyası oluşturur ve her jpg görüntüleri yüz algılandı.

| Aşama | Dosya adı | Notlar |
| --- | --- | --- |
| Giriş varlık |foo.bar |Video WMV, MPV veya MP4 biçimindeki |
| Giriş yapılandırma |İş yapılandırması hazır |{'version':'1.0 ', 'Seçenekler': {'modu': 'çözümleyin'}} |
| Çıkış varlık |foo_annotations.JSON |Ek açıklama verileri JSON biçiminde yüz konumu. Bu, hello kullanıcı toomodify hello sınırlayıcı kutular Bulanıklaştırma tarafından düzenlenebilir. Aşağıdaki örneğe bakın. |
| Çıkış varlık |foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg] |Yüz burada hello numarası hello labelId hello yazıtipinin gösterir, her kırpılmış jpg algılandı |

#### <a name="output-example"></a>Çıkış örneği:

    {
      "version": 1,
      "timescale": 24000,
      "offset": 0,
      "framerate": 23.976,
      "width": 1280,
      "height": 720,
      "fragments": [
        {
          "start": 0,
          "duration": 48048,
          "interval": 1001,
          "events": [
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [
              {
                "index": 13,
                "id": 1138,
                "x": 0.29537,
                "y": -0.18987,
                "width": 0.36239,
                "height": 0.80335
              },
              {
                "index": 13,
                "id": 2028,
                "x": 0.60427,
                "y": 0.16098,
                "width": 0.26958,
                "height": 0.57943
              }
            ],

    … truncated

### <a name="redact-mode"></a>Mod Redaksiyon
Merhaba ikinci geçişi hello iş akışının çok sayıda tek bir varlığa birleştirilmelidir girişleri alır.

Bu kimlikleri tooblur, hello özgün video ve hello ek açıklamaları JSON listesini içerir. Bu mod hello ek açıklamaları tooapply hello giriş video Bulanıklaştırma kullanır.

Merhaba hello Çözümle geçişi çıktısını hello özgün video içermez. Merhaba video hello giriş varlık hello Redact modu görev için içine yüklenir ve hello birincil dosya olarak seçili toobe gerekir.

| Aşama | Dosya adı | Notlar |
| --- | --- | --- |
| Giriş varlık |foo.bar |Video WMV, MPV veya MP4 biçimindeki. Aynı 1. adım olduğu gibi video. |
| Giriş varlık |foo_annotations.JSON |meta veri dosyasından birinci aşaması, isteğe bağlı değişiklik yapılması açısından ek açıklamaları. |
| Giriş varlık |foo_IDList.txt (isteğe bağlı) |İsteğe bağlı yeni bir satırla ayrılmış yüz kimlikleri tooredact listesi. Boş bırakılırsa, bu tüm yüzeyleri bulanıklaştırır. |
| Giriş yapılandırma |İş yapılandırması hazır |{'version':'1.0 ', 'Seçenekler': {'modu': 'Redaksiyon'}} |
| Çıkış varlık |foo_redacted.mp4 |Ek açıklamalar uygulanan Bulanıklaştırma ile video dayalı |

#### <a name="example-output"></a>Örnek çıktı
Seçili bir Kimliğine sahip bir IDList hello çıktısını budur.

[Bu videoyu izleyin](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

Örnek foo_IDList.txt
 
     1
     2
     3

## <a name="blur-types"></a>Türleri ölçeklendirilmelidir

Merhaba, **birleştirilmiş** veya **Redact** modu, seçim yapabileceğiniz hello JSON giriş yapılandırılması yoluyla 5 farklı Bulanıklaştırma modu vardır: **düşük**, **Med**, **Yüksek**, **hata ayıklama**, ve **siyah**. Varsayılan olarak **Med** kullanılır.

Merhaba örnekleri türleri aşağıdaki ölçeklendirilmelidir bulabilirsiniz.

### <a name="example-json"></a>Örnek JSON:

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a>Düşük

![Düşük](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a>MED

![MED](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a>Yüksek

![Yüksek](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a>Hata ayıklama

![Hata ayıklama](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a>Siyah

![Siyah](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-hello-output-json-file"></a>Merhaba çıkış JSON dosyasının öğeleri

Merhaba Redaksiyon MP Yüksek duyarlılık yüz konumu algılama ve video çerçevesinde too64 İnsan Yüz Yukarı algılayabilir izleme sağlar. Tamamen çıplak yüzeyleri yan yüz ve küçük yazıtipleri hello en iyi sonuçlar sağlayın (değerinden büyük veya eşit too24x24 piksel) zor olan.

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a>.NET örnek kod

Merhaba aşağıdaki program gösterir nasıl yapılır:

1. Bir varlık oluşturun ve hello varlığa bir medya dosyasını yükleyin.
2. Json hazır aşağıdaki hello içeren bir yapılandırma dosyasına dayalı yüz Redaksiyon görevle ilgili bir iş oluşturun. 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
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

    namespace FaceRedaction
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

            // Run hello FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download hello job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload hello input media file toostorage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference tooAzure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from hello specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with hello encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify hello input asset.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

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

## <a name="next-steps"></a>Sonraki adımlar

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>İlgili bağlantılar
[Azure Media Services Analytics a genel bakış](media-services-analytics-overview.md)

[Azure medya analizi gösterileri](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

