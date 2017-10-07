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
#  <a name="use-azure-media-encoder-standard-tooauto-generate-a-bitrate-ladder"></a><span data-ttu-id="ad9b4-105">Azure Medya Kodlayıcısı standart tooauto kullanın-bit hızı Merdiveni oluştur</span><span class="sxs-lookup"><span data-stu-id="ad9b4-105">Use Azure Media Encoder Standard tooauto-generate a bitrate ladder</span></span>

## <a name="overview"></a><span data-ttu-id="ad9b4-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="ad9b4-106">Overview</span></span>

<span data-ttu-id="ad9b4-107">Bu konuda gösterilmektedir nasıl toouse Medya Kodlayıcısı standart (MES) tooauto-hello giriş çözünürlük ve bit hızı dayalı bir bit hızı Merdiveni (bit hızı çözümleme çiftleri) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ad9b4-107">This topic shows how toouse Media Encoder Standard (MES) tooauto-generate a bitrate ladder (bitrate-resolution pairs) based on hello input resolution and bitrate.</span></span> <span data-ttu-id="ad9b4-108">Merhaba otomatik olarak oluşturulan hazır hiç giriş hello çözünürlük ve bit hızı aşacak.</span><span class="sxs-lookup"><span data-stu-id="ad9b4-108">hello auto-generated preset will never exceed hello input resolution and bitrate.</span></span> <span data-ttu-id="ad9b4-109">Örneğin, hello giriş olması durumunda 3 MB/sn, çıktı adresindeki 720p 720 p en iyi kalır ve 3 MB/sn düşük hızlarında başlar.</span><span class="sxs-lookup"><span data-stu-id="ad9b4-109">For example, if hello input is 720p at 3Mbps, output will remain 720p at best, and will start at rates lower than 3Mbps.</span></span>

### <a name="encoding-for-streaming-only"></a><span data-ttu-id="ad9b4-110">Yalnızca akış için kodlama</span><span class="sxs-lookup"><span data-stu-id="ad9b4-110">Encoding for Streaming Only</span></span>

<span data-ttu-id="ad9b4-111">Maksadınızı tooencode ise, kaynak, sınırlandırmak kullanın sonra hello "Uyarlamalı akış" yalnızca akış için video kodlama bir görev oluştururken hazır.</span><span class="sxs-lookup"><span data-stu-id="ad9b4-111">If your intent is tooencode your source video only for streaming, then you shoud use hello "Adaptive Streaming" preset when creating an encoding task.</span></span> <span data-ttu-id="ad9b4-112">Merhaba kullanırken **Uyarlamalı akış** hazır hello MES Kodlayıcı akıllıca bit hızı Merdiveni cap.</span><span class="sxs-lookup"><span data-stu-id="ad9b4-112">When using hello **Adaptive Streaming** preset, hello MES encoder will intelligently cap a bitrate ladder.</span></span> <span data-ttu-id="ad9b4-113">Ancak, bu yana hello hizmeti kaç katmanları toouse belirler ve hangi çözünürlükte maliyetleri kodlama mümkün toocontrol hello olmaz.</span><span class="sxs-lookup"><span data-stu-id="ad9b4-113">However, you will not be able toocontrol hello encoding costs, since hello service determines how many layers toouse and at what resolution.</span></span> <span data-ttu-id="ad9b4-114">Örnek ile Merhaba kodlama sonucunda MES tarafından üretilen çıkış katmanların görebilirsiniz **Uyarlamalı akış** hello bu konunun sonunda hazır.</span><span class="sxs-lookup"><span data-stu-id="ad9b4-114">You can see examples of output layers produced by MES as a result of encoding with hello **Adaptive Streaming** preset at hello end of this topic.</span></span> <span data-ttu-id="ad9b4-115">Merhaba, varlık MP4 dosyaları ses burada içerir ve video değil araya çıktı.</span><span class="sxs-lookup"><span data-stu-id="ad9b4-115">hello output Asset will contain MP4 files where audio and video are not interleaved.</span></span>

### <a name="encoding-for-streaming-and-progressive-download"></a><span data-ttu-id="ad9b4-116">Akış ve aşamalı indirme kodlama</span><span class="sxs-lookup"><span data-stu-id="ad9b4-116">Encoding for Streaming and Progressive Download</span></span>

<span data-ttu-id="ad9b4-117">Maksadınızı tooencode ise, sınırlandırmak kullanın sonra "İçerik Uyarlamalı Çoklu bit hızlı MP4" Merhaba tooproduce MP4 dosyalarını aşamalı indirmek yanı sıra akış için kaynak videonuzu kodlama bir görev oluştururken hazır.</span><span class="sxs-lookup"><span data-stu-id="ad9b4-117">If your intent is tooencode your source video for streaming as well as tooproduce MP4 files for progressive download, then you shoud use hello "Content Adaptive Multiple Bitrate MP4" preset when creating an encoding task.</span></span> <span data-ttu-id="ad9b4-118">Merhaba kullanırken **içerik Uyarlamalı Çoklu bit hızlı MP4** hello MES Kodlayıcı aynı kodlama mantığı yukarıdaki gibi ancak hello çıkış varlığına MP4 içerecek artık dosyaları ses burada hello geçerli ve video araya eklemeli hazır.</span><span class="sxs-lookup"><span data-stu-id="ad9b4-118">When using hello **Content Adaptive Multiple Bitrate MP4** preset, hello MES encoder will apply hello same encoding logic as above, but now hello output asset will contain MP4 files where audio and video are interleaved.</span></span> <span data-ttu-id="ad9b4-119">Aşamalı indirme dosyası olarak bu MP4 dosyaları (örneğin, hello yüksek bit hızı sürüm) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad9b4-119">You can use one of these MP4 files (for example, hello highest bitrate version) as a progressive download file.</span></span>

## <span data-ttu-id="ad9b4-120"><a id="encoding_with_dotnet"></a>Media Services .NET SDK'sı ile kodlama</span><span class="sxs-lookup"><span data-stu-id="ad9b4-120"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="ad9b4-121">Aşağıdaki kod örneğine hello görevleri aşağıdaki Media Services .NET SDK'sı tooperform hello kullanır:</span><span class="sxs-lookup"><span data-stu-id="ad9b4-121">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

- <span data-ttu-id="ad9b4-122">Bir kodlama işi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ad9b4-122">Create an encoding job.</span></span>
- <span data-ttu-id="ad9b4-123">Bir başvuru toohello Medya Kodlayıcısı standart Kodlayıcısı alın.</span><span class="sxs-lookup"><span data-stu-id="ad9b4-123">Get a reference toohello Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="ad9b4-124">Bir kodlama görev toohello işi ekleyebilir ve toouse hello **Uyarlamalı akış** hazır.</span><span class="sxs-lookup"><span data-stu-id="ad9b4-124">Add an encoding task toohello job and specify toouse hello **Adaptive Streaming** preset.</span></span> 
- <span data-ttu-id="ad9b4-125">Kodlanmış hello varlık içerecek bir çıkış varlığı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ad9b4-125">Create an output asset that will contain hello encoded asset.</span></span>
- <span data-ttu-id="ad9b4-126">Bir olay işleyicisi toocheck hello ilerleyişini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ad9b4-126">Add an event handler toocheck hello job progress.</span></span>
- <span data-ttu-id="ad9b4-127">Merhaba işi gönderin.</span><span class="sxs-lookup"><span data-stu-id="ad9b4-127">Submit hello job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="ad9b4-128">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ad9b4-128">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="ad9b4-129">Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="ad9b4-129">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="ad9b4-130">Örnek</span><span class="sxs-lookup"><span data-stu-id="ad9b4-130">Example</span></span>

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

## <span data-ttu-id="ad9b4-131"><a id="output"></a>Çıktı</span><span class="sxs-lookup"><span data-stu-id="ad9b4-131"><a id="output"></a>Output</span></span>

<span data-ttu-id="ad9b4-132">Bu bölümde üç örnekleri ile Merhaba kodlama sonucunda MES tarafından üretilen çıkış Katmanlar gösterilmiştir **Uyarlamalı akış** hazır.</span><span class="sxs-lookup"><span data-stu-id="ad9b4-132">This section shows three examples of output layers produced by MES as a result of encoding with hello **Adaptive Streaming** preset.</span></span> 

### <a name="example-1"></a><span data-ttu-id="ad9b4-133">Örnek 1</span><span class="sxs-lookup"><span data-stu-id="ad9b4-133">Example 1</span></span>
<span data-ttu-id="ad9b4-134">Yükseklik "1080" ve "29.970" kare hızı kaynağıyla 6 video katmanları üretir:</span><span class="sxs-lookup"><span data-stu-id="ad9b4-134">Source with height "1080" and framerate "29.970" produces 6 video layers:</span></span>

|<span data-ttu-id="ad9b4-135">Katman</span><span class="sxs-lookup"><span data-stu-id="ad9b4-135">Layer</span></span>|<span data-ttu-id="ad9b4-136">Yükseklik</span><span class="sxs-lookup"><span data-stu-id="ad9b4-136">Height</span></span>|<span data-ttu-id="ad9b4-137">Genişlik</span><span class="sxs-lookup"><span data-stu-id="ad9b4-137">Width</span></span>|<span data-ttu-id="ad9b4-138">Bitrate(Kbps)</span><span class="sxs-lookup"><span data-stu-id="ad9b4-138">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="ad9b4-139">1</span><span class="sxs-lookup"><span data-stu-id="ad9b4-139">1</span></span>|<span data-ttu-id="ad9b4-140">1080</span><span class="sxs-lookup"><span data-stu-id="ad9b4-140">1080</span></span>|<span data-ttu-id="ad9b4-141">1920</span><span class="sxs-lookup"><span data-stu-id="ad9b4-141">1920</span></span>|<span data-ttu-id="ad9b4-142">6780</span><span class="sxs-lookup"><span data-stu-id="ad9b4-142">6780</span></span>|
|<span data-ttu-id="ad9b4-143">2</span><span class="sxs-lookup"><span data-stu-id="ad9b4-143">2</span></span>|<span data-ttu-id="ad9b4-144">720</span><span class="sxs-lookup"><span data-stu-id="ad9b4-144">720</span></span>|<span data-ttu-id="ad9b4-145">1280</span><span class="sxs-lookup"><span data-stu-id="ad9b4-145">1280</span></span>|<span data-ttu-id="ad9b4-146">3520</span><span class="sxs-lookup"><span data-stu-id="ad9b4-146">3520</span></span>|
|<span data-ttu-id="ad9b4-147">3</span><span class="sxs-lookup"><span data-stu-id="ad9b4-147">3</span></span>|<span data-ttu-id="ad9b4-148">540</span><span class="sxs-lookup"><span data-stu-id="ad9b4-148">540</span></span>|<span data-ttu-id="ad9b4-149">960</span><span class="sxs-lookup"><span data-stu-id="ad9b4-149">960</span></span>|<span data-ttu-id="ad9b4-150">2210</span><span class="sxs-lookup"><span data-stu-id="ad9b4-150">2210</span></span>|
|<span data-ttu-id="ad9b4-151">4</span><span class="sxs-lookup"><span data-stu-id="ad9b4-151">4</span></span>|<span data-ttu-id="ad9b4-152">360</span><span class="sxs-lookup"><span data-stu-id="ad9b4-152">360</span></span>|<span data-ttu-id="ad9b4-153">640</span><span class="sxs-lookup"><span data-stu-id="ad9b4-153">640</span></span>|<span data-ttu-id="ad9b4-154">1150</span><span class="sxs-lookup"><span data-stu-id="ad9b4-154">1150</span></span>|
|<span data-ttu-id="ad9b4-155">5</span><span class="sxs-lookup"><span data-stu-id="ad9b4-155">5</span></span>|<span data-ttu-id="ad9b4-156">270</span><span class="sxs-lookup"><span data-stu-id="ad9b4-156">270</span></span>|<span data-ttu-id="ad9b4-157">480</span><span class="sxs-lookup"><span data-stu-id="ad9b4-157">480</span></span>|<span data-ttu-id="ad9b4-158">720</span><span class="sxs-lookup"><span data-stu-id="ad9b4-158">720</span></span>|
|<span data-ttu-id="ad9b4-159">6</span><span class="sxs-lookup"><span data-stu-id="ad9b4-159">6</span></span>|<span data-ttu-id="ad9b4-160">180</span><span class="sxs-lookup"><span data-stu-id="ad9b4-160">180</span></span>|<span data-ttu-id="ad9b4-161">320</span><span class="sxs-lookup"><span data-stu-id="ad9b4-161">320</span></span>|<span data-ttu-id="ad9b4-162">380</span><span class="sxs-lookup"><span data-stu-id="ad9b4-162">380</span></span>|

### <a name="example-2"></a><span data-ttu-id="ad9b4-163">Örnek 2</span><span class="sxs-lookup"><span data-stu-id="ad9b4-163">Example 2</span></span>
<span data-ttu-id="ad9b4-164">Yükseklik "720" ve "23.970" kare hızı kaynağıyla 5 video katmanları üretir:</span><span class="sxs-lookup"><span data-stu-id="ad9b4-164">Source with height "720" and framerate "23.970" produces 5 video layers:</span></span>

|<span data-ttu-id="ad9b4-165">Katman</span><span class="sxs-lookup"><span data-stu-id="ad9b4-165">Layer</span></span>|<span data-ttu-id="ad9b4-166">Yükseklik</span><span class="sxs-lookup"><span data-stu-id="ad9b4-166">Height</span></span>|<span data-ttu-id="ad9b4-167">Genişlik</span><span class="sxs-lookup"><span data-stu-id="ad9b4-167">Width</span></span>|<span data-ttu-id="ad9b4-168">Bitrate(Kbps)</span><span class="sxs-lookup"><span data-stu-id="ad9b4-168">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="ad9b4-169">1</span><span class="sxs-lookup"><span data-stu-id="ad9b4-169">1</span></span>|<span data-ttu-id="ad9b4-170">720</span><span class="sxs-lookup"><span data-stu-id="ad9b4-170">720</span></span>|<span data-ttu-id="ad9b4-171">1280</span><span class="sxs-lookup"><span data-stu-id="ad9b4-171">1280</span></span>|<span data-ttu-id="ad9b4-172">2940</span><span class="sxs-lookup"><span data-stu-id="ad9b4-172">2940</span></span>|
|<span data-ttu-id="ad9b4-173">2</span><span class="sxs-lookup"><span data-stu-id="ad9b4-173">2</span></span>|<span data-ttu-id="ad9b4-174">540</span><span class="sxs-lookup"><span data-stu-id="ad9b4-174">540</span></span>|<span data-ttu-id="ad9b4-175">960</span><span class="sxs-lookup"><span data-stu-id="ad9b4-175">960</span></span>|<span data-ttu-id="ad9b4-176">1850</span><span class="sxs-lookup"><span data-stu-id="ad9b4-176">1850</span></span>|
|<span data-ttu-id="ad9b4-177">3</span><span class="sxs-lookup"><span data-stu-id="ad9b4-177">3</span></span>|<span data-ttu-id="ad9b4-178">360</span><span class="sxs-lookup"><span data-stu-id="ad9b4-178">360</span></span>|<span data-ttu-id="ad9b4-179">640</span><span class="sxs-lookup"><span data-stu-id="ad9b4-179">640</span></span>|<span data-ttu-id="ad9b4-180">960</span><span class="sxs-lookup"><span data-stu-id="ad9b4-180">960</span></span>|
|<span data-ttu-id="ad9b4-181">4</span><span class="sxs-lookup"><span data-stu-id="ad9b4-181">4</span></span>|<span data-ttu-id="ad9b4-182">270</span><span class="sxs-lookup"><span data-stu-id="ad9b4-182">270</span></span>|<span data-ttu-id="ad9b4-183">480</span><span class="sxs-lookup"><span data-stu-id="ad9b4-183">480</span></span>|<span data-ttu-id="ad9b4-184">600</span><span class="sxs-lookup"><span data-stu-id="ad9b4-184">600</span></span>|
|<span data-ttu-id="ad9b4-185">5</span><span class="sxs-lookup"><span data-stu-id="ad9b4-185">5</span></span>|<span data-ttu-id="ad9b4-186">180</span><span class="sxs-lookup"><span data-stu-id="ad9b4-186">180</span></span>|<span data-ttu-id="ad9b4-187">320</span><span class="sxs-lookup"><span data-stu-id="ad9b4-187">320</span></span>|<span data-ttu-id="ad9b4-188">320</span><span class="sxs-lookup"><span data-stu-id="ad9b4-188">320</span></span>|

### <a name="example-3"></a><span data-ttu-id="ad9b4-189">Örnek 3</span><span class="sxs-lookup"><span data-stu-id="ad9b4-189">Example 3</span></span>
<span data-ttu-id="ad9b4-190">Yükseklik "360" ve "29.970" kare hızı kaynağıyla 3 video katmanları üretir:</span><span class="sxs-lookup"><span data-stu-id="ad9b4-190">Source with height "360" and framerate "29.970" produces 3 video layers:</span></span>

|<span data-ttu-id="ad9b4-191">Katman</span><span class="sxs-lookup"><span data-stu-id="ad9b4-191">Layer</span></span>|<span data-ttu-id="ad9b4-192">Yükseklik</span><span class="sxs-lookup"><span data-stu-id="ad9b4-192">Height</span></span>|<span data-ttu-id="ad9b4-193">Genişlik</span><span class="sxs-lookup"><span data-stu-id="ad9b4-193">Width</span></span>|<span data-ttu-id="ad9b4-194">Bitrate(Kbps)</span><span class="sxs-lookup"><span data-stu-id="ad9b4-194">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="ad9b4-195">1</span><span class="sxs-lookup"><span data-stu-id="ad9b4-195">1</span></span>|<span data-ttu-id="ad9b4-196">360</span><span class="sxs-lookup"><span data-stu-id="ad9b4-196">360</span></span>|<span data-ttu-id="ad9b4-197">640</span><span class="sxs-lookup"><span data-stu-id="ad9b4-197">640</span></span>|<span data-ttu-id="ad9b4-198">700</span><span class="sxs-lookup"><span data-stu-id="ad9b4-198">700</span></span>|
|<span data-ttu-id="ad9b4-199">2</span><span class="sxs-lookup"><span data-stu-id="ad9b4-199">2</span></span>|<span data-ttu-id="ad9b4-200">270</span><span class="sxs-lookup"><span data-stu-id="ad9b4-200">270</span></span>|<span data-ttu-id="ad9b4-201">480</span><span class="sxs-lookup"><span data-stu-id="ad9b4-201">480</span></span>|<span data-ttu-id="ad9b4-202">440</span><span class="sxs-lookup"><span data-stu-id="ad9b4-202">440</span></span>|
|<span data-ttu-id="ad9b4-203">3</span><span class="sxs-lookup"><span data-stu-id="ad9b4-203">3</span></span>|<span data-ttu-id="ad9b4-204">180</span><span class="sxs-lookup"><span data-stu-id="ad9b4-204">180</span></span>|<span data-ttu-id="ad9b4-205">320</span><span class="sxs-lookup"><span data-stu-id="ad9b4-205">320</span></span>|<span data-ttu-id="ad9b4-206">230</span><span class="sxs-lookup"><span data-stu-id="ad9b4-206">230</span></span>|
## <a name="media-services-learning-paths"></a><span data-ttu-id="ad9b4-207">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="ad9b4-207">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ad9b4-208">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="ad9b4-208">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="ad9b4-209">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ad9b4-209">See Also</span></span>
[<span data-ttu-id="ad9b4-210">Media Services kodlama a genel bakış</span><span class="sxs-lookup"><span data-stu-id="ad9b4-210">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

