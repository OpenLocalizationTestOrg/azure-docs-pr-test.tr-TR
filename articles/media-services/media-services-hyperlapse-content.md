---
title: "aaaHyperlapse Azure medya Hyperlapse ile medya dosyalarını | Microsoft Docs"
description: "Azure medya Hyperlapse kesintisiz zaman onlara videolar ilk kişi veya eylem kamera içeriğini oluşturur. Bu konuda gösterilmektedir nasıl toouse medya dizin oluşturucu."
services: media-services
documentationcenter: 
author: asolanki
manager: johndeu
editor: 
ms.assetid: 37d54db6-9cf3-4ae9-b3c6-0d29c744e965
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/02/2017
ms.author: adsolank
ms.openlocfilehash: 85bb07206d0ca2f5b2fd0767e6ed4904195d3ab6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a>Azure medya Hyperlapse ile medya dosyalarını
Azure medya Hyperlapse bir medya işlemci (ilk kişi veya eylem kamera içerikten kesintisiz zaman onlara videolar oluşturan MP) olur.  bulut tabanlı eşdüzey çok hello[Microsoft Research'ın masaüstü Hyperlapse Pro ve telefon tabanlı Hyperlapse Mobile](http://aka.ms/hyperlapse), Azure Media Services için Microsoft Hyperlapse hello yoğun hello Azure Media Services medya ölçeğini kullanır Platform toohorizontally işleme ölçeğini ve toplu paralel hale Hyperlapse işleme.

> [!IMPORTANT]
> Microsoft Hyperlapse tasarlanmış toowork taşıma kamera ilk kişinin içerikle en iyi olur.  Halen kamera görüntülerinin çalışmaya devam ancak hello performansına ve kalitesine ilişkin hello Azure medya Hyperlapse medya işlemcisi diğer içerik türleri için garanti edilemez.  toolearn Azure Media Services için Microsoft Hyperlapse hakkında daha fazla bilgi ve bazı örnek videolar bakın, hello denetleyin [giriş blog gönderisi](http://aka.ms/azurehyperlapseblog) hello public preview sürümünden.
> 
> 

İş geçen olarak bir Azure medya Hyperlapse giriş hangi çerçeveler videonun zaman onlara gerektiğini belirtir yapılandırma dosyası ve toowhat hızı yanı sıra bir MP4, MOV veya WMV varlık dosyası (örn. ilk 10.000 çerçeve 2 x).  Merhaba çıkışı sabit ve zaman onlara yorumlama hello giriş videonun yapılır.

Merhaba en son Azure medya Hyperlapse güncelleştirmeler için bkz: [Media Services bloglar](https://azure.microsoft.com/blog/topics/media-services/).

## <a name="hyperlapse-an-asset"></a>Hyperlapse bir varlığı
Öncelikle, istenen giriş dosyası tooAzure Media Services tooupload gerekir.  karşıya yükleme ve içeriği yönetme ile ilgili kavramları hakkında daha fazla bilgi toolearn hello okuma hello [içerik yönetimi makale](media-services-portal-vod-get-started.md).

### <a id="configuration"></a>Hyperlapse yapılandırma hazır
İçeriğinizi Media Services hesabınızı eklendiğinde, yapılandırmanızı önceden tooconstruct gerekir.  Aşağıdaki tablonun hello hello kullanıcı tanımlı alanlar açıklanmaktadır:

| Alan | Açıklama |
| --- | --- |
| StartFrame |Merhaba çerçeve işleme hangi hello Microsoft Hyperlapse başlamalısınız. |
| NumFrames |Çerçeve tooprocess Hello sayısı |
| Hız |hangi toospeed hello giriş video yukarı faktörüyle Hello. |

Merhaba, XML ve JSON uyumluluğunu yapılandırma dosyası örneği verilmiştir:

**XML hazır:**

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

**JSON hazır:**

    {
        "Version":1.0,
        "Sources": [
            {
                "StartFrame":0,
                "NumFrames":2147483647
            }
        ],
        "Options": {
            "Speed":1,
            "Stabilize":false
        }
    }

### <a id="sample_code"></a>Microsoft Hyperlapse hello AMS .NET SDK'sı ile
Merhaba aşağıdaki yöntemi bir medya dosya bir varlık olarak yükler ve hello ile Azure medya Hyperlapse medya işlemcisi bir işi oluşturur.

> [!NOTE]
> Bu kod toowork kapsamına hello adı "context" ile bir CloudMediaContext olmanız gerekir.  Bu, okuma hello hakkında daha fazla toolearn [içerik yönetimi makale](media-services-dotnet-get-started.md).
> 
> [!NOTE]
> Merhaba dize bağımsız değişkeni "hyperConfig" JSON ya da yukarıda açıklandığı gibi XML uyumluluğunu yapılandırma önceden beklenen toobe ' dir.
> 
> 

        static bool RunHyperlapseJob(string input, string output, string hyperConfig)
        {
            // create asset with input file
            IAsset asset = context
            .Assets
            .CreateAssetAndUploadSingleFile(input, "My Hyperlapse Input", AssetCreationOptions.None);

            // grab instances of Azure Media Hyperlapse MP
            IMediaProcessor mp = context
            .MediaProcessors
            .GetLatestMediaProcessorByName("Azure Media Hyperlapse");

            // create Job with Hyperlapse task
            IJob job = context
            .Jobs
            .Create(String.Format("Hyperlapse {0}", input));

            if (String.IsNullOrEmpty(hyperConfig))
            {
            // config cannot be empty
            return false;
            }

            hyperConfig = File.ReadAllText(hyperConfig);

            ITask hyperlapseTask = job.Tasks.AddNew("Hyperlapse task",
            mp,
            hyperConfig,
            TaskOptions.None);
            hyperlapseTask.InputAssets.Add(asset);
            hyperlapseTask.OutputAssets.AddNew("Hyperlapse output",
            AssetCreationOptions.None);

            job.Submit();

            // Create progress printing and querying tasks
            Task progressPrintTask = new Task(() =>
            {

            IJob jobQuery = null;
            do
            {
                var progressContext = context;
                jobQuery = progressContext.Jobs
                .Where(j => j.Id == job.Id)
                .First();
                Console.WriteLine(string.Format("{0}\t{1}\t{2}",
                DateTime.Now,
                jobQuery.State,
                jobQuery.Tasks[0].Progress));
                Thread.Sleep(10000);
            }
            while (jobQuery.State != JobState.Finished &&
                                   jobQuery.State != JobState.Error &&
                                   jobQuery.State != JobState.Canceled);
                });
                
            progressPrintTask.Start();

            Task progressJobTask = job.GetExecutionProgressTask(
                                                 CancellationToken.None);
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
                return false;                  
            }

        DownloadAsset(job.OutputMediaAssets.First(), output);
        return true;
    }

    static void DownloadAsset(IAsset asset, string outputDirectory)
    {
        foreach (IAssetFile file in asset.AssetFiles)
        {
            file.Download(Path.Combine(outputDirectory, file.Name));
        }
    }


    static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
    {
        IAsset asset = context.Assets.Create(assetName, options);

        var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
        assetFile.Upload(filePath);

        return asset;
    }

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = context.MediaProcessors
        .Where(p => p.Name == mediaProcessorName)
        .ToList()
        .OrderBy(p => new Version(p.Version))
        .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }

### <a id="file_types"></a>Desteklenen dosya türleri
* MP4
* MOV
* WMV

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>İlgili bağlantılar
[Azure Media Services Analytics a genel bakış](media-services-analytics-overview.md)

[Azure medya analizi gösterileri](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

