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
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a><span data-ttu-id="75be5-104">Azure medya Hyperlapse ile medya dosyalarını</span><span class="sxs-lookup"><span data-stu-id="75be5-104">Hyperlapse Media Files with Azure Media Hyperlapse</span></span>
<span data-ttu-id="75be5-105">Azure medya Hyperlapse bir medya işlemci (ilk kişi veya eylem kamera içerikten kesintisiz zaman onlara videolar oluşturan MP) olur.</span><span class="sxs-lookup"><span data-stu-id="75be5-105">Azure Media Hyperlapse is a Media Processor (MP) that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="75be5-106">bulut tabanlı eşdüzey çok hello[Microsoft Research'ın masaüstü Hyperlapse Pro ve telefon tabanlı Hyperlapse Mobile](http://aka.ms/hyperlapse), Azure Media Services için Microsoft Hyperlapse hello yoğun hello Azure Media Services medya ölçeğini kullanır Platform toohorizontally işleme ölçeğini ve toplu paralel hale Hyperlapse işleme.</span><span class="sxs-lookup"><span data-stu-id="75be5-106">hello cloud-based sibling too[Microsoft Research's desktop Hyperlapse Pro and phone-based Hyperlapse Mobile](http://aka.ms/hyperlapse), Microsoft Hyperlapse for Azure Media Services utilizes hello massive scale of hello Azure Media Services Media Processing platform toohorizontally scale and parallelize bulk Hyperlapse processing.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="75be5-107">Microsoft Hyperlapse tasarlanmış toowork taşıma kamera ilk kişinin içerikle en iyi olur.</span><span class="sxs-lookup"><span data-stu-id="75be5-107">Microsoft Hyperlapse is designed toowork best on first-person content with a moving camera.</span></span>  <span data-ttu-id="75be5-108">Halen kamera görüntülerinin çalışmaya devam ancak hello performansına ve kalitesine ilişkin hello Azure medya Hyperlapse medya işlemcisi diğer içerik türleri için garanti edilemez.</span><span class="sxs-lookup"><span data-stu-id="75be5-108">Although still-camera footage can still work, hello performance and quality of hello Azure Media Hyperlapse Media Processor cannot be guaranteed for other types of content.</span></span>  <span data-ttu-id="75be5-109">toolearn Azure Media Services için Microsoft Hyperlapse hakkında daha fazla bilgi ve bazı örnek videolar bakın, hello denetleyin [giriş blog gönderisi](http://aka.ms/azurehyperlapseblog) hello public preview sürümünden.</span><span class="sxs-lookup"><span data-stu-id="75be5-109">toolearn more about Microsoft Hyperlapse for Azure Media Services and see some example videos, check out hello [introductory blog post](http://aka.ms/azurehyperlapseblog) from hello public preview.</span></span>
> 
> 

<span data-ttu-id="75be5-110">İş geçen olarak bir Azure medya Hyperlapse giriş hangi çerçeveler videonun zaman onlara gerektiğini belirtir yapılandırma dosyası ve toowhat hızı yanı sıra bir MP4, MOV veya WMV varlık dosyası (örn. ilk 10.000 çerçeve 2 x).</span><span class="sxs-lookup"><span data-stu-id="75be5-110">An Azure Media Hyperlapse job takes as input an MP4, MOV, or WMV asset file along with a configuration file that specifies which frames of video should be time-lapsed and toowhat speed (e.g. first 10,000 frames at 2x).</span></span>  <span data-ttu-id="75be5-111">Merhaba çıkışı sabit ve zaman onlara yorumlama hello giriş videonun yapılır.</span><span class="sxs-lookup"><span data-stu-id="75be5-111">hello output is a stabilized and time-lapsed rendition of hello input video.</span></span>

<span data-ttu-id="75be5-112">Merhaba en son Azure medya Hyperlapse güncelleştirmeler için bkz: [Media Services bloglar](https://azure.microsoft.com/blog/topics/media-services/).</span><span class="sxs-lookup"><span data-stu-id="75be5-112">For hello latest Azure Media Hyperlapse updates, see [Media Services blogs](https://azure.microsoft.com/blog/topics/media-services/).</span></span>

## <a name="hyperlapse-an-asset"></a><span data-ttu-id="75be5-113">Hyperlapse bir varlığı</span><span class="sxs-lookup"><span data-stu-id="75be5-113">Hyperlapse an asset</span></span>
<span data-ttu-id="75be5-114">Öncelikle, istenen giriş dosyası tooAzure Media Services tooupload gerekir.</span><span class="sxs-lookup"><span data-stu-id="75be5-114">First you will need tooupload your desired input file tooAzure Media Services.</span></span>  <span data-ttu-id="75be5-115">karşıya yükleme ve içeriği yönetme ile ilgili kavramları hakkında daha fazla bilgi toolearn hello okuma hello [içerik yönetimi makale](media-services-portal-vod-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="75be5-115">toolearn more about hello concepts involved with uploading and managing content, read hello [content management article](media-services-portal-vod-get-started.md).</span></span>

### <span data-ttu-id="75be5-116"><a id="configuration"></a>Hyperlapse yapılandırma hazır</span><span class="sxs-lookup"><span data-stu-id="75be5-116"><a id="configuration"></a>Configuration Preset for Hyperlapse</span></span>
<span data-ttu-id="75be5-117">İçeriğinizi Media Services hesabınızı eklendiğinde, yapılandırmanızı önceden tooconstruct gerekir.</span><span class="sxs-lookup"><span data-stu-id="75be5-117">Once your content is in your Media Services account, you will need tooconstruct your configuration preset.</span></span>  <span data-ttu-id="75be5-118">Aşağıdaki tablonun hello hello kullanıcı tanımlı alanlar açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="75be5-118">hello following table explains hello user-specified fields:</span></span>

| <span data-ttu-id="75be5-119">Alan</span><span class="sxs-lookup"><span data-stu-id="75be5-119">Field</span></span> | <span data-ttu-id="75be5-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="75be5-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="75be5-121">StartFrame</span><span class="sxs-lookup"><span data-stu-id="75be5-121">StartFrame</span></span> |<span data-ttu-id="75be5-122">Merhaba çerçeve işleme hangi hello Microsoft Hyperlapse başlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="75be5-122">hello frame upon which hello Microsoft Hyperlapse processing should begin.</span></span> |
| <span data-ttu-id="75be5-123">NumFrames</span><span class="sxs-lookup"><span data-stu-id="75be5-123">NumFrames</span></span> |<span data-ttu-id="75be5-124">Çerçeve tooprocess Hello sayısı</span><span class="sxs-lookup"><span data-stu-id="75be5-124">hello number of frames tooprocess</span></span> |
| <span data-ttu-id="75be5-125">Hız</span><span class="sxs-lookup"><span data-stu-id="75be5-125">Speed</span></span> |<span data-ttu-id="75be5-126">hangi toospeed hello giriş video yukarı faktörüyle Hello.</span><span class="sxs-lookup"><span data-stu-id="75be5-126">hello factor with which toospeed up hello input video.</span></span> |

<span data-ttu-id="75be5-127">Merhaba, XML ve JSON uyumluluğunu yapılandırma dosyası örneği verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="75be5-127">hello following is an example of a conformant configuration file in XML and JSON:</span></span>

<span data-ttu-id="75be5-128">**XML hazır:**</span><span class="sxs-lookup"><span data-stu-id="75be5-128">**XML preset:**</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

<span data-ttu-id="75be5-129">**JSON hazır:**</span><span class="sxs-lookup"><span data-stu-id="75be5-129">**JSON preset:**</span></span>

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

### <span data-ttu-id="75be5-130"><a id="sample_code"></a>Microsoft Hyperlapse hello AMS .NET SDK'sı ile</span><span class="sxs-lookup"><span data-stu-id="75be5-130"><a id="sample_code"></a> Microsoft Hyperlapse with hello AMS .NET SDK</span></span>
<span data-ttu-id="75be5-131">Merhaba aşağıdaki yöntemi bir medya dosya bir varlık olarak yükler ve hello ile Azure medya Hyperlapse medya işlemcisi bir işi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="75be5-131">hello following method uploads a media file as an asset and creates a job with hello Azure Media Hyperlapse Media Processor.</span></span>

> [!NOTE]
> <span data-ttu-id="75be5-132">Bu kod toowork kapsamına hello adı "context" ile bir CloudMediaContext olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="75be5-132">You should already have a CloudMediaContext in scope with hello name "context" for this code toowork.</span></span>  <span data-ttu-id="75be5-133">Bu, okuma hello hakkında daha fazla toolearn [içerik yönetimi makale](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="75be5-133">toolearn more about this, read hello [content management article](media-services-dotnet-get-started.md).</span></span>
> 
> [!NOTE]
> <span data-ttu-id="75be5-134">Merhaba dize bağımsız değişkeni "hyperConfig" JSON ya da yukarıda açıklandığı gibi XML uyumluluğunu yapılandırma önceden beklenen toobe ' dir.</span><span class="sxs-lookup"><span data-stu-id="75be5-134">hello string argument "hyperConfig" is expected toobe a conformant configuration preset in either JSON or XML as described above.</span></span>
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

### <span data-ttu-id="75be5-135"><a id="file_types"></a>Desteklenen dosya türleri</span><span class="sxs-lookup"><span data-stu-id="75be5-135"><a id="file_types"></a>Supported File types</span></span>
* <span data-ttu-id="75be5-136">MP4</span><span class="sxs-lookup"><span data-stu-id="75be5-136">MP4</span></span>
* <span data-ttu-id="75be5-137">MOV</span><span class="sxs-lookup"><span data-stu-id="75be5-137">MOV</span></span>
* <span data-ttu-id="75be5-138">WMV</span><span class="sxs-lookup"><span data-stu-id="75be5-138">WMV</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="75be5-139">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="75be5-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="75be5-140">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="75be5-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="75be5-141">İlgili bağlantılar</span><span class="sxs-lookup"><span data-stu-id="75be5-141">Related links</span></span>
[<span data-ttu-id="75be5-142">Azure Media Services Analytics a genel bakış</span><span class="sxs-lookup"><span data-stu-id="75be5-142">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="75be5-143">Azure medya analizi gösterileri</span><span class="sxs-lookup"><span data-stu-id="75be5-143">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

