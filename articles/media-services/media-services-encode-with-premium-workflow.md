---
title: "Medya Kodlayıcısı Premium akışıyla aaaAdvanced kodlama | Microsoft Docs"
description: "Bilgi nasıl Medya Kodlayıcısı Premium akışıyla tooencode. Kod örnekleri C# dilinde yazılmıştır ve .NET için Media Services SDK'sı hello kullanın."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 0f4c87ac-810a-4d42-8df8-923dff2016c6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 5a1c3d019a5c8fbf9bda2da751a7eff4c4907d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-encoding-with-media-encoder-premium-workflow"></a><span data-ttu-id="c1dea-104">Medya Kodlayıcısı Premium akışıyla kodlama Gelişmiş</span><span class="sxs-lookup"><span data-stu-id="c1dea-104">Advanced encoding with Media Encoder Premium Workflow</span></span>
> [!NOTE]
> <span data-ttu-id="c1dea-105">Bu konuda tartışılan Medya Kodlayıcısı Premium iş akışı medya işlemcisi Çin'de kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="c1dea-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span>
>
>

<span data-ttu-id="c1dea-106">Premium Kodlayıcı sorular için mepd adresindeki Microsoft.com e-posta.</span><span class="sxs-lookup"><span data-stu-id="c1dea-106">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="overview"></a><span data-ttu-id="c1dea-107">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="c1dea-107">Overview</span></span>
<span data-ttu-id="c1dea-108">Microsoft Azure Media Services hello Tanıtımı **Medya Kodlayıcısı Premium iş akışı** medya işlemcisi.</span><span class="sxs-lookup"><span data-stu-id="c1dea-108">Microsoft Azure Media Services is introducing hello **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="c1dea-109">Bu işlemci teklifleri Gelişmiş özellikleri, premium isteğe bağlı iş akışları için kodlama.</span><span class="sxs-lookup"><span data-stu-id="c1dea-109">This processor offers advance encoding capabilities for your premium on-demand workflows.</span></span>

<span data-ttu-id="c1dea-110">Merhaba aşağıdaki konular anahat çok ilgili ayrıntıları**Medya Kodlayıcısı Premium iş akışı**:</span><span class="sxs-lookup"><span data-stu-id="c1dea-110">hello following topics outline details related too**Media Encoder Premium Workflow**:</span></span>

* <span data-ttu-id="c1dea-111">[Merhaba Medya Kodlayıcısı Premium iş akışı tarafından desteklenen biçimler](media-services-premium-workflow-encoder-formats.md) – anlatılmaktadır hello dosya biçimlerini ve tarafından desteklenen codec bileşenleri **Medya Kodlayıcısı Premium iş akışı**.</span><span class="sxs-lookup"><span data-stu-id="c1dea-111">[Formats Supported by hello Media Encoder Premium Workflow](media-services-premium-workflow-encoder-formats.md) – Discusses hello file formats and codecs supported by **Media Encoder Premium Workflow**.</span></span>
* <span data-ttu-id="c1dea-112">[Genel bakış ve Azure karşılaştırma isteğe bağlı medya kodlayıcılar üzerine](media-services-encode-asset.md) karşılaştırır hello kodlama yeteneklerini **Medya Kodlayıcısı Premium iş akışı** ve **Medya Kodlayıcısı standart**.</span><span class="sxs-lookup"><span data-stu-id="c1dea-112">[Overview and comparison of Azure on demand media encoders](media-services-encode-asset.md) compares hello encoding capabilities of **Media Encoder Premium Workflow** and **Media Encoder Standard**.</span></span>

<span data-ttu-id="c1dea-113">Bu konuda gösterilir nasıl tooencode ile **Medya Kodlayıcısı Premium iş akışı** .NET kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c1dea-113">This topic demonstrates how tooencode with **Media Encoder Premium Workflow** using .NET.</span></span>

<span data-ttu-id="c1dea-114">Merhaba görevlerde kodlama **Medya Kodlayıcısı Premium iş akışı** bir iş akışı dosyası adlı bir ayrı yapılandırma dosyası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c1dea-114">Encoding tasks for hello **Media Encoder Premium Workflow** require a separate configuration file, called a Workflow file.</span></span> <span data-ttu-id="c1dea-115">Bu dosyalar .workflow uzantısına sahiptir ve hello kullanılarak oluşturulan [iş akışı Tasarımcısı](media-services-workflow-designer.md) aracı.</span><span class="sxs-lookup"><span data-stu-id="c1dea-115">These files have a .workflow extension and are created using hello [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

<span data-ttu-id="c1dea-116">Merhaba varsayılan iş akışı dosyalarını alabilir [burada](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span><span class="sxs-lookup"><span data-stu-id="c1dea-116">You can also get hello default workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span></span> <span data-ttu-id="c1dea-117">Başlangıç klasörü de bu dosyaları hello açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="c1dea-117">hello folder also contains hello description of these files.</span></span>

<span data-ttu-id="c1dea-118">Merhaba iş akışı dosyalarını karşıya toobe tooyour Media Services hesabı bir varlık olarak gerekir ve bu varlık görev kodlama toohello geçirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c1dea-118">hello workflow files need toobe uploaded tooyour Media Services account as an Asset, and this Asset should be passed in toohello encoding Task.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="c1dea-119">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c1dea-119">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="c1dea-120">Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="c1dea-120">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="encoding-example"></a><span data-ttu-id="c1dea-121">Kodlama örneği</span><span class="sxs-lookup"><span data-stu-id="c1dea-121">Encoding example</span></span>

<span data-ttu-id="c1dea-122">Merhaba aşağıdaki örnekte gösterilmiştir nasıl tooencode ile **Medya Kodlayıcısı Premium iş akışı**.</span><span class="sxs-lookup"><span data-stu-id="c1dea-122">hello following example demonstrates how tooencode with **Media Encoder Premium Workflow**.</span></span>

<span data-ttu-id="c1dea-123">Aşağıdaki adımları hello gerçekleştirilir:</span><span class="sxs-lookup"><span data-stu-id="c1dea-123">hello following steps are performed:</span></span>

1. <span data-ttu-id="c1dea-124">Bir varlık oluşturun ve bir iş akışı dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c1dea-124">Create an asset and upload a workflow file.</span></span>
2. <span data-ttu-id="c1dea-125">Bir varlık oluşturun ve bir kaynak medya dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c1dea-125">Create an asset and upload a source media file.</span></span>
3. <span data-ttu-id="c1dea-126">Merhaba "Medya Kodlayıcısı Premium iş akışı" medya işlemcisi alın.</span><span class="sxs-lookup"><span data-stu-id="c1dea-126">Get hello "Media Encoder Premium Workflow" media processor.</span></span>
4. <span data-ttu-id="c1dea-127">Bir işi ve bir görev oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c1dea-127">Create a job and a task.</span></span>

    <span data-ttu-id="c1dea-128">Çoğu durumda, hello yapılandırma dizesi hello görev için boştur (aşağıdaki örneğine hello ister).</span><span class="sxs-lookup"><span data-stu-id="c1dea-128">In most cases, hello configuration string for hello task is empty (like in hello following example).</span></span> <span data-ttu-id="c1dea-129">(Tootooset çalışma zamanı özellikleri dinamik olarak gerektirir) bazı Gelişmiş senaryolar vardır; bu durumda bir XML dizesi toohello kodlama görevi sağlar.</span><span class="sxs-lookup"><span data-stu-id="c1dea-129">There are some advanced scenarios (that require you tootooset runtime properties dynamically) in which case you would provide an XML string toohello encoding task.</span></span> <span data-ttu-id="c1dea-130">Bu tür senaryoların örnekleri şunlardır: bir katmana, Dikiş, subtitling paralel veya sıralı medya oluşturma.</span><span class="sxs-lookup"><span data-stu-id="c1dea-130">Examples of such scenarios are: creating an overlay, parallel or sequential media stitching, subtitling.</span></span>
5. <span data-ttu-id="c1dea-131">İki giriş varlıklar toohello görev ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c1dea-131">Add two input assets toohello task.</span></span>

    1. <span data-ttu-id="c1dea-132">1 – hello iş akışı varlık.</span><span class="sxs-lookup"><span data-stu-id="c1dea-132">1st – hello workflow asset.</span></span>
    2. <span data-ttu-id="c1dea-133">2 – hello varlığı.</span><span class="sxs-lookup"><span data-stu-id="c1dea-133">2nd – hello video asset.</span></span>

    >[!NOTE]
    ><span data-ttu-id="c1dea-134">Merhaba iş akışı varlık toohello görev hello medya varlık önce eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c1dea-134">hello workflow asset must be added toohello task before hello media asset.</span></span>
   <span data-ttu-id="c1dea-135">Bu görev için Hello yapılandırma dizesi boş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c1dea-135">hello configuration string for this task should be empty.</span></span>
   
6. <span data-ttu-id="c1dea-136">Merhaba kodlama işi gönderin.</span><span class="sxs-lookup"><span data-stu-id="c1dea-136">Submit hello encoding job.</span></span>

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using System.Threading.Tasks;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderPremiumWorkflowSample
        {
            class Program
            {
                private static readonly string _AADTenantDomain =
                    ConfigurationManager.AppSettings["AADTenantDomain"];
                private static readonly string _RESTAPIEndpoint =
                    ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

                // Field for service context.
                private static CloudMediaContext _context = null;

                private static readonly string _supportFiles =
                    Path.GetFullPath(@"../..\Media");

                private static readonly string _workflowFilePath =
                    Path.GetFullPath(_supportFiles + @"\H264 Progressive Download MP4.workflow");

                private static readonly string _singleMP4InputFilePath =
                    Path.GetFullPath(_supportFiles + @"\BigBuckBunny.mp4");

                static void Main(string[] args)
                {
                    var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                    _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                    var workflowAsset = CreateAssetAndUploadSingleFile(_workflowFilePath);
                    var videoAsset = CreateAssetAndUploadSingleFile(_singleMP4InputFilePath);
                    IAsset outputAsset = CreateEncodingJob(workflowAsset, videoAsset);

                }

                static public IAsset CreateAssetAndUploadSingleFile(string singleFilePath)
                {
                    var assetName = "UploadSingleFile_" + DateTime.UtcNow.ToString();
                    var asset = _context.Assets.Create(assetName, AssetCreationOptions.None);

                    var fileName = Path.GetFileName(singleFilePath);

                    var assetFile = asset.AssetFiles.Create(fileName);

                    Console.WriteLine("Created assetFile {0}", assetFile.Name);

                    Console.WriteLine("Upload {0}", assetFile.Name);

                    assetFile.Upload(singleFilePath);
                    Console.WriteLine("Done uploading {0}", assetFile.Name);

                    return asset;
                }

                static public IAsset CreateEncodingJob(IAsset workflow, IAsset video)
                {
                    // Declare a new job.
                    IJob job = _context.Jobs.Create("Premium Workflow encoding job");
                    // Get a media processor reference, and pass tooit hello name of the
                    // processor toouse for hello specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

                    // Create a task with hello encoding details, using a string preset.
                    ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                        processor,
                        "",
                        TaskOptions.None);

                    // Specify hello input asset toobe encoded.
                    task.InputAssets.Add(workflow);
                    task.InputAssets.Add(video); // we add one asset
                                                 // Add an output asset toocontain hello results of hello job.
                                                 // This output is specified as AssetCreationOptions.None, which
                                                 // means hello output asset is not encrypted.
                    task.OutputAssets.AddNew("Output asset",
                        AssetCreationOptions.None);

                    // Use hello following event handler toocheck job progress.  
                    job.StateChanged += new
                            EventHandler<JobStateChangedEventArgs>(StateChanged);

                    // Launch hello job.
                    job.Submit();

                    // Check job execution and wait for job toofinish.
                    Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
                    progressJobTask.Wait();

                    // If job state is Error hello event handling
                    // method for job progress should log errors.  Here we check
                    // for error state and exit if needed.
                    if (job.State == JobState.Error)
                    {
                        throw new Exception("\nExiting method due toojob error.");
                    }

                    return job.OutputMediaAssets[0];
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

<span data-ttu-id="c1dea-137">Premium Kodlayıcı sorular için mepd adresindeki Microsoft.com e-posta.</span><span class="sxs-lookup"><span data-stu-id="c1dea-137">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="c1dea-138">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="c1dea-138">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c1dea-139">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="c1dea-139">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
