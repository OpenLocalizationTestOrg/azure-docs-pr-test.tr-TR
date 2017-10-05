---
title: "Medya Kodlayıcısı Premium akışıyla kodlama Gelişmiş | Microsoft Docs"
description: "Medya Kodlayıcısı Premium akışıyla kodlamak öğrenin. Kod örnekleri, C# dilinde yazılmıştır ve .NET için Media Services SDK'sını kullanın."
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
ms.openlocfilehash: 2b03853bf07e05c07fd730d5e8a8563963887921
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="advanced-encoding-with-media-encoder-premium-workflow"></a><span data-ttu-id="c3a15-104">Medya Kodlayıcısı Premium akışıyla kodlama Gelişmiş</span><span class="sxs-lookup"><span data-stu-id="c3a15-104">Advanced encoding with Media Encoder Premium Workflow</span></span>
> [!NOTE]
> <span data-ttu-id="c3a15-105">Bu konuda tartışılan Medya Kodlayıcısı Premium iş akışı medya işlemcisi Çin'de kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="c3a15-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span>
>
>

<span data-ttu-id="c3a15-106">Premium Kodlayıcı sorular için mepd adresindeki Microsoft.com e-posta.</span><span class="sxs-lookup"><span data-stu-id="c3a15-106">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="overview"></a><span data-ttu-id="c3a15-107">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="c3a15-107">Overview</span></span>
<span data-ttu-id="c3a15-108">Microsoft Azure Media Services Tanıtımı **Medya Kodlayıcısı Premium iş akışı** medya işlemcisi.</span><span class="sxs-lookup"><span data-stu-id="c3a15-108">Microsoft Azure Media Services is introducing the **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="c3a15-109">Bu işlemci teklifleri Gelişmiş özellikleri, premium isteğe bağlı iş akışları için kodlama.</span><span class="sxs-lookup"><span data-stu-id="c3a15-109">This processor offers advance encoding capabilities for your premium on-demand workflows.</span></span>

<span data-ttu-id="c3a15-110">Aşağıdaki konular ilgili ayrıntıları anahat **Medya Kodlayıcısı Premium iş akışı**:</span><span class="sxs-lookup"><span data-stu-id="c3a15-110">The following topics outline details related to **Media Encoder Premium Workflow**:</span></span>

* <span data-ttu-id="c3a15-111">[Medya Kodlayıcısı Premium iş akışı tarafından desteklenen biçimler](media-services-premium-workflow-encoder-formats.md) – Discusses dosya biçimlerini ve desteklenen codec bileşenleri tarafından **Medya Kodlayıcısı Premium iş akışı**.</span><span class="sxs-lookup"><span data-stu-id="c3a15-111">[Formats Supported by the Media Encoder Premium Workflow](media-services-premium-workflow-encoder-formats.md) – Discusses the file formats and codecs supported by **Media Encoder Premium Workflow**.</span></span>
* <span data-ttu-id="c3a15-112">[Genel bakış ve Azure karşılaştırma isteğe bağlı medya kodlayıcılar üzerine](media-services-encode-asset.md) kodlama özelliklerini karşılaştırır **Medya Kodlayıcısı Premium iş akışı** ve **Medya Kodlayıcısı standart**.</span><span class="sxs-lookup"><span data-stu-id="c3a15-112">[Overview and comparison of Azure on demand media encoders](media-services-encode-asset.md) compares the encoding capabilities of **Media Encoder Premium Workflow** and **Media Encoder Standard**.</span></span>

<span data-ttu-id="c3a15-113">Bu konu ile kodlamak gösterilmiştir **Medya Kodlayıcısı Premium iş akışı** .NET kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c3a15-113">This topic demonstrates how to encode with **Media Encoder Premium Workflow** using .NET.</span></span>

<span data-ttu-id="c3a15-114">Görevler için kodlama **Medya Kodlayıcısı Premium iş akışı** bir iş akışı dosyası adlı bir ayrı yapılandırma dosyası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c3a15-114">Encoding tasks for the **Media Encoder Premium Workflow** require a separate configuration file, called a Workflow file.</span></span> <span data-ttu-id="c3a15-115">Bu dosyalar .workflow uzantısına sahiptir ve kullanılarak oluşturulan [iş akışı Tasarımcısı](media-services-workflow-designer.md) aracı.</span><span class="sxs-lookup"><span data-stu-id="c3a15-115">These files have a .workflow extension and are created using the [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

<span data-ttu-id="c3a15-116">Varsayılan iş akışı dosyalarını alabilir [burada](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span><span class="sxs-lookup"><span data-stu-id="c3a15-116">You can also get the default workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span></span> <span data-ttu-id="c3a15-117">Klasör, bu dosyaların açıklaması da içerir.</span><span class="sxs-lookup"><span data-stu-id="c3a15-117">The folder also contains the description of these files.</span></span>

<span data-ttu-id="c3a15-118">Bir varlık olarak Media Services hesabınıza karşıya yüklenecek iş akışı dosyalarını gerekir ve bu varlık kodlama görevi geçirilmesi.</span><span class="sxs-lookup"><span data-stu-id="c3a15-118">The workflow files need to be uploaded to your Media Services account as an Asset, and this Asset should be passed in to the encoding Task.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="c3a15-119">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c3a15-119">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="c3a15-120">Geliştirme ortamınızı kurun ve app.config dosyanızı [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md) bölümünde açıklandığı gibi bağlantı bilgileriyle doldurun.</span><span class="sxs-lookup"><span data-stu-id="c3a15-120">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="encoding-example"></a><span data-ttu-id="c3a15-121">Kodlama örneği</span><span class="sxs-lookup"><span data-stu-id="c3a15-121">Encoding example</span></span>

<span data-ttu-id="c3a15-122">Aşağıdaki örnek ile kodlamak gösterilmiştir **Medya Kodlayıcısı Premium iş akışı**.</span><span class="sxs-lookup"><span data-stu-id="c3a15-122">The following example demonstrates how to encode with **Media Encoder Premium Workflow**.</span></span>

<span data-ttu-id="c3a15-123">Aşağıdaki adımlar gerçekleştirilir:</span><span class="sxs-lookup"><span data-stu-id="c3a15-123">The following steps are performed:</span></span>

1. <span data-ttu-id="c3a15-124">Bir varlık oluşturun ve bir iş akışı dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c3a15-124">Create an asset and upload a workflow file.</span></span>
2. <span data-ttu-id="c3a15-125">Bir varlık oluşturun ve bir kaynak medya dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c3a15-125">Create an asset and upload a source media file.</span></span>
3. <span data-ttu-id="c3a15-126">"Medya Kodlayıcısı Premium iş akışı" medya işlemcisi alın.</span><span class="sxs-lookup"><span data-stu-id="c3a15-126">Get the "Media Encoder Premium Workflow" media processor.</span></span>
4. <span data-ttu-id="c3a15-127">Bir işi ve bir görev oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c3a15-127">Create a job and a task.</span></span>

    <span data-ttu-id="c3a15-128">Çoğu durumda, görev için yapılandırma dizesi boştur (aşağıdaki örnekte ister).</span><span class="sxs-lookup"><span data-stu-id="c3a15-128">In most cases, the configuration string for the task is empty (like in the following example).</span></span> <span data-ttu-id="c3a15-129">(İçin çalışma zamanı özellikleri dinamik olarak ayarlamak gerekir) bazı Gelişmiş senaryolar vardır; bu durumda kodlama görev bir XML dizesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="c3a15-129">There are some advanced scenarios (that require you to to set runtime properties dynamically) in which case you would provide an XML string to the encoding task.</span></span> <span data-ttu-id="c3a15-130">Bu tür senaryoların örnekleri şunlardır: bir katmana, Dikiş, subtitling paralel veya sıralı medya oluşturma.</span><span class="sxs-lookup"><span data-stu-id="c3a15-130">Examples of such scenarios are: creating an overlay, parallel or sequential media stitching, subtitling.</span></span>
5. <span data-ttu-id="c3a15-131">İki giriş varlıklar göreve ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c3a15-131">Add two input assets to the task.</span></span>

    1. <span data-ttu-id="c3a15-132">1 – iş akışı varlık.</span><span class="sxs-lookup"><span data-stu-id="c3a15-132">1st – the workflow asset.</span></span>
    2. <span data-ttu-id="c3a15-133">2 – varlığı.</span><span class="sxs-lookup"><span data-stu-id="c3a15-133">2nd – the video asset.</span></span>

    >[!NOTE]
    ><span data-ttu-id="c3a15-134">İş akışı varlık görev medya varlık önce eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3a15-134">The workflow asset must be added to the task before the media asset.</span></span>
   <span data-ttu-id="c3a15-135">Bu görev için yapılandırma dizesi boş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c3a15-135">The configuration string for this task should be empty.</span></span>
   
6. <span data-ttu-id="c3a15-136">Kodlama işinin gönderin.</span><span class="sxs-lookup"><span data-stu-id="c3a15-136">Submit the encoding job.</span></span>

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
                    // Get a media processor reference, and pass to it the name of the
                    // processor to use for the specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

                    // Create a task with the encoding details, using a string preset.
                    ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                        processor,
                        "",
                        TaskOptions.None);

                    // Specify the input asset to be encoded.
                    task.InputAssets.Add(workflow);
                    task.InputAssets.Add(video); // we add one asset
                                                 // Add an output asset to contain the results of the job.
                                                 // This output is specified as AssetCreationOptions.None, which
                                                 // means the output asset is not encrypted.
                    task.OutputAssets.AddNew("Output asset",
                        AssetCreationOptions.None);

                    // Use the following event handler to check job progress.  
                    job.StateChanged += new
                            EventHandler<JobStateChangedEventArgs>(StateChanged);

                    // Launch the job.
                    job.Submit();

                    // Check job execution and wait for job to finish.
                    Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
                    progressJobTask.Wait();

                    // If job state is Error the event handling
                    // method for job progress should log errors.  Here we check
                    // for error state and exit if needed.
                    if (job.State == JobState.Error)
                    {
                        throw new Exception("\nExiting method due to job error.");
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

<span data-ttu-id="c3a15-137">Premium Kodlayıcı sorular için mepd adresindeki Microsoft.com e-posta.</span><span class="sxs-lookup"><span data-stu-id="c3a15-137">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="c3a15-138">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="c3a15-138">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c3a15-139">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="c3a15-139">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
