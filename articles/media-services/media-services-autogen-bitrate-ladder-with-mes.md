---
title: "aaaUse Azure Medya Kodlayıcısı standart tooauto-bit hızı Merdiveni oluştur | Microsoft Docs"
description: "Bu konuda gösterilmektedir nasıl toouse Medya Kodlayıcısı standart (MES) tooauto-hello giriş çözünürlük ve bit hızı dayalı bir bit hızı Merdiveni oluşturur. Merhaba giriş çözünürlük ve bit hızı hiçbir zaman aşacak. Örneğin, hello giriş olması durumunda 3 MB/sn, çıktı adresindeki 720p 720 p en iyi kalır ve 3 MB/sn düşük hızlarında başlar."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 63ed95da-1b82-44b0-b8ff-eebd535bc5c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 5437f54ac28c42ddd4f9d1986549d6da6261c5da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
#  <a name="use-azure-media-encoder-standard-tooauto-generate-a-bitrate-ladder"></a>Azure Medya Kodlayıcısı standart tooauto kullanın-bit hızı Merdiveni oluştur

## <a name="overview"></a>Genel Bakış

Bu konuda gösterilmektedir nasıl toouse Medya Kodlayıcısı standart (MES) tooauto-hello giriş çözünürlük ve bit hızı dayalı bir bit hızı Merdiveni (bit hızı çözümleme çiftleri) oluşturur. Merhaba otomatik olarak oluşturulan hazır hiç giriş hello çözünürlük ve bit hızı aşacak. Örneğin, hello giriş olması durumunda 3 MB/sn, çıktı adresindeki 720p 720 p en iyi kalır ve 3 MB/sn düşük hızlarında başlar.

### <a name="encoding-for-streaming-only"></a>Yalnızca akış için kodlama

Maksadınızı tooencode ise, kaynak, sınırlandırmak kullanın sonra hello "Uyarlamalı akış" yalnızca akış için video kodlama bir görev oluştururken hazır. Merhaba kullanırken **Uyarlamalı akış** hazır hello MES Kodlayıcı akıllıca bit hızı Merdiveni cap. Ancak, bu yana hello hizmeti kaç katmanları toouse belirler ve hangi çözünürlükte maliyetleri kodlama mümkün toocontrol hello olmaz. Örnek ile Merhaba kodlama sonucunda MES tarafından üretilen çıkış katmanların görebilirsiniz **Uyarlamalı akış** hello bu konunun sonunda hazır. Merhaba, varlık MP4 dosyaları ses burada içerir ve video değil araya çıktı.

### <a name="encoding-for-streaming-and-progressive-download"></a>Akış ve aşamalı indirme kodlama

Maksadınızı tooencode ise, sınırlandırmak kullanın sonra "İçerik Uyarlamalı Çoklu bit hızlı MP4" Merhaba tooproduce MP4 dosyalarını aşamalı indirmek yanı sıra akış için kaynak videonuzu kodlama bir görev oluştururken hazır. Merhaba kullanırken **içerik Uyarlamalı Çoklu bit hızlı MP4** hello MES Kodlayıcı aynı kodlama mantığı yukarıdaki gibi ancak hello çıkış varlığına MP4 içerecek artık dosyaları ses burada hello geçerli ve video araya eklemeli hazır. Aşamalı indirme dosyası olarak bu MP4 dosyaları (örneğin, hello yüksek bit hızı sürüm) kullanabilirsiniz.

## <a id="encoding_with_dotnet"></a>Media Services .NET SDK'sı ile kodlama

Aşağıdaki kod örneğine hello görevleri aşağıdaki Media Services .NET SDK'sı tooperform hello kullanır:

- Bir kodlama işi oluşturun.
- Bir başvuru toohello Medya Kodlayıcısı standart Kodlayıcısı alın.
- Bir kodlama görev toohello işi ekleyebilir ve toouse hello **Uyarlamalı akış** hazır. 
- Kodlanmış hello varlık içerecek bir çıkış varlığı oluşturun.
- Bir olay işleyicisi toocheck hello ilerleyişini ekleyin.
- Merhaba işi gönderin.

#### <a name="create-and-configure-a-visual-studio-project"></a>Visual Studio projesi oluşturup yapılandırma

Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Örnek

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreamingMESPresest
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

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate hello output using hello "Adaptive Streaming" preset.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");

            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
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

## <a id="output"></a>Çıktı

Bu bölümde üç örnekleri ile Merhaba kodlama sonucunda MES tarafından üretilen çıkış Katmanlar gösterilmiştir **Uyarlamalı akış** hazır. 

### <a name="example-1"></a>Örnek 1
Yükseklik "1080" ve "29.970" kare hızı kaynağıyla 6 video katmanları üretir:

|Katman|Yükseklik|Genişlik|Bitrate(Kbps)|
|---|---|---|---|
|1|1080|1920|6780|
|2|720|1280|3520|
|3|540|960|2210|
|4|360|640|1150|
|5|270|480|720|
|6|180|320|380|

### <a name="example-2"></a>Örnek 2
Yükseklik "720" ve "23.970" kare hızı kaynağıyla 5 video katmanları üretir:

|Katman|Yükseklik|Genişlik|Bitrate(Kbps)|
|---|---|---|---|
|1|720|1280|2940|
|2|540|960|1850|
|3|360|640|960|
|4|270|480|600|
|5|180|320|320|

### <a name="example-3"></a>Örnek 3
Yükseklik "360" ve "29.970" kare hızı kaynağıyla 3 video katmanları üretir:

|Katman|Yükseklik|Genişlik|Bitrate(Kbps)|
|---|---|---|---|
|1|360|640|700|
|2|270|480|440|
|3|180|320|230|
## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Ayrıca Bkz.
[Media Services kodlama a genel bakış](media-services-encode-asset.md)

