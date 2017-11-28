---
title: "aaaEncode Medya Kodlayıcısı .NET kullanarak standart bir varlıkla | Microsoft Docs"
description: "Bu konuda gösterilmektedir nasıl toouse .NET tooencode medya Kodlayıcı standart kullanarak bir varlık."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 03431b64-5518-478a-a1c2-1de345999274
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 25e274c3b67168f4afc8b8ab04af2d654c9dd6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a><span data-ttu-id="a8d95-103">Bir varlık Medya Kodlayıcısı .NET kullanarak standart ile kodlamak</span><span class="sxs-lookup"><span data-stu-id="a8d95-103">Encode an asset with Media Encoder Standard using .NET</span></span>
<span data-ttu-id="a8d95-104">Kodlama işleri hello en yaygın işlemleri Media Services biridir.</span><span class="sxs-lookup"><span data-stu-id="a8d95-104">Encoding jobs are one of hello most common processing operations in Media Services.</span></span> <span data-ttu-id="a8d95-105">Bir kodlama tooanother kodlama işleri tooconvert medya dosyaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a8d95-105">You create encoding jobs tooconvert media files from one encoding tooanother.</span></span> <span data-ttu-id="a8d95-106">Kodlarken, hello Media Services yerleşik medya kodlayıcı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8d95-106">When you encode, you can use hello Media Services built-in Media Encoder.</span></span> <span data-ttu-id="a8d95-107">Bir Media Services iş ortağı tarafından sağlanan bir kodlayıcı de kullanabilirsiniz; üçüncü taraf kodlayıcılar hello Azure Market kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a8d95-107">You can also use an encoder provided by a Media Services partner; third party encoders are available through hello Azure Marketplace.</span></span> 

<span data-ttu-id="a8d95-108">Bu konuda gösterilmektedir nasıl toouse .NET tooencode varlıklarınızı ile Medya Kodlayıcısı standart (MES).</span><span class="sxs-lookup"><span data-stu-id="a8d95-108">This topic shows how toouse .NET tooencode your assets with Media Encoder Standard (MES).</span></span> <span data-ttu-id="a8d95-109">Medya Kodlayıcısı standart yapılandırılmış açıklanan hello Kodlayıcı hazır birini kullanarak [burada](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="a8d95-109">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

<span data-ttu-id="a8d95-110">Tooalways Kaynak dosyalarınız Uyarlamalı bit hızlı MP4 kümesi kodlamak ve hello kullanarak hello kümesi toohello istenen biçimine dönüştür önerilen [dinamik paketleme](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a8d95-110">It is recommended tooalways encode your source files into an adaptive bitrate MP4 set and then convert hello set toohello desired format using hello [Dynamic Packaging](media-services-dynamic-packaging-overview.md).</span></span> 

<span data-ttu-id="a8d95-111">Çıkış varlığına depolama şifrelenmiş ise, varlık teslim ilkesini yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8d95-111">If your output asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="a8d95-112">Daha fazla bilgi için bkz: [varlık teslim ilkesini yapılandırma](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="a8d95-112">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a8d95-113">Bir çıkış dosyası içeren bir ad ile Merhaba ilk 32 karakteri MES üretir girdi dosyası adı hello.</span><span class="sxs-lookup"><span data-stu-id="a8d95-113">MES produces an output file with a name that contains hello first 32 characters of hello input file name.</span></span> <span data-ttu-id="a8d95-114">Merhaba ad hello hazır dosyasında belirtilen üzerinde temel alır.</span><span class="sxs-lookup"><span data-stu-id="a8d95-114">hello name is based on what is specified in hello preset file.</span></span> <span data-ttu-id="a8d95-115">Örneğin, "dosya adı": "{Basename} _ {Index} {uzantısı}".</span><span class="sxs-lookup"><span data-stu-id="a8d95-115">For example, "FileName": "{Basename}_{Index}{Extension}".</span></span> <span data-ttu-id="a8d95-116">{Basename} hello tarafından değiştirilir hello giriş dosyası adının ilk 32 karakteri.</span><span class="sxs-lookup"><span data-stu-id="a8d95-116">{Basename} is replaced by hello first 32 characters of hello input file name.</span></span>
> 
> 

### <a name="mes-formats"></a><span data-ttu-id="a8d95-117">MES biçimleri</span><span class="sxs-lookup"><span data-stu-id="a8d95-117">MES Formats</span></span>
[<span data-ttu-id="a8d95-118">Biçimleri ve codec bileşenleri</span><span class="sxs-lookup"><span data-stu-id="a8d95-118">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a><span data-ttu-id="a8d95-119">MES Ön ayarları</span><span class="sxs-lookup"><span data-stu-id="a8d95-119">MES Presets</span></span>
<span data-ttu-id="a8d95-120">Medya Kodlayıcısı standart yapılandırılmış açıklanan hello Kodlayıcı hazır birini kullanarak [burada](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="a8d95-120">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="a8d95-121">Giriş ve çıkış meta verileri</span><span class="sxs-lookup"><span data-stu-id="a8d95-121">Input and output metadata</span></span>
<span data-ttu-id="a8d95-122">Bir giriş varlık (veya varlıklar) MES kullanarak kodlarken bir çıkış varlığı edinme hello başarılı şekilde tamamlandığını, kodlama görev.</span><span class="sxs-lookup"><span data-stu-id="a8d95-122">When you encode an input asset (or assets) using MES, you get an output asset at hello successful completion of that encode task.</span></span> <span data-ttu-id="a8d95-123">Merhaba çıkış varlık, video, ses, küçük resimleri, bildirimi, kullandığınız hello kodlama hazır ayarına göre göre vb. içerir.</span><span class="sxs-lookup"><span data-stu-id="a8d95-123">hello output asset contains video, audio, thumbnails, manifest, etc. based on hello encoding preset you use.</span></span>

<span data-ttu-id="a8d95-124">Merhaba çıkış varlığına hello giriş varlık hakkındaki meta verileri sahip bir dosya da içerir.</span><span class="sxs-lookup"><span data-stu-id="a8d95-124">hello output asset also contains a file with metadata about hello input asset.</span></span> <span data-ttu-id="a8d95-125">Merhaba hello meta veri XML dosyası adına sahip biçimini izleyen hello: < asset_id > _metadata.xml (örneğin, 41114ad3-eb5e - 4 c 57-8 d 92-5354e2b7d4a4_metadata.xml), burada < asset_id > değeridir hello AssetID hello giriş varlık.</span><span class="sxs-lookup"><span data-stu-id="a8d95-125">hello name of hello metadata XML file has hello following format: <asset_id>_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where <asset_id> is hello AssetId value of hello input asset.</span></span> <span data-ttu-id="a8d95-126">Merhaba giriş bu meta veri XML Şeması açıklanan [burada](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="a8d95-126">hello schema of this input metadata XML is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="a8d95-127">Merhaba çıkış varlığına hello çıkış varlık hakkındaki meta verileri sahip bir dosya da içerir.</span><span class="sxs-lookup"><span data-stu-id="a8d95-127">hello output asset also contains a file with metadata about hello output asset.</span></span> <span data-ttu-id="a8d95-128">Merhaba hello meta veri XML dosyası adına sahip biçimini izleyen hello: < source_file_name > _manifest.xml (örneğin, BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="a8d95-128">hello name of hello metadata XML file has hello following format: <source_file_name>_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span> <span data-ttu-id="a8d95-129">XML açıklanmıştır Bu çıktı meta verileri Hello şeması [burada](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="a8d95-129">hello schema of this output metadata XML is described [here](media-services-output-metadata-schema.md).</span></span>

<span data-ttu-id="a8d95-130">Merhaba iki meta veri dosyalarının herhangi birini tooexamine istiyorsanız, bir SAS Bulucu oluşturmanız ve hello dosya tooyour yerel bilgisayara indirin.</span><span class="sxs-lookup"><span data-stu-id="a8d95-130">If you want tooexamine either of hello two metadata files, you can create a SAS locator and download hello file tooyour local computer.</span></span> <span data-ttu-id="a8d95-131">Toocreate bir SAS Bulucu ve yükleme dosyasını kullanarak hello medya hizmetleri nasıl üzerinde bir örnek bulabilirsiniz .NET SDK uzantıları.</span><span class="sxs-lookup"><span data-stu-id="a8d95-131">You can find an example on how toocreate a SAS locator and download a file Using hello Media Services .NET SDK Extensions.</span></span>

## <a name="download-sample"></a><span data-ttu-id="a8d95-132">Örnek indirme</span><span class="sxs-lookup"><span data-stu-id="a8d95-132">Download sample</span></span>
<span data-ttu-id="a8d95-133">Alın ve gösteren bir örnek çalıştırın nasıl MES ile tooencode [burada](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="a8d95-133">You can get and run a sample that shows how tooencode with MES from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="a8d95-134">.NET örnek kod</span><span class="sxs-lookup"><span data-stu-id="a8d95-134">.NET sample code</span></span>

<span data-ttu-id="a8d95-135">Aşağıdaki kod örneğine hello görevleri aşağıdaki Media Services .NET SDK'sı tooperform hello kullanır:</span><span class="sxs-lookup"><span data-stu-id="a8d95-135">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

* <span data-ttu-id="a8d95-136">Bir kodlama işi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a8d95-136">Create an encoding job.</span></span>
* <span data-ttu-id="a8d95-137">Bir başvuru toohello Medya Kodlayıcısı standart Kodlayıcısı alın.</span><span class="sxs-lookup"><span data-stu-id="a8d95-137">Get a reference toohello Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="a8d95-138">Toouse hello belirtin [Uyarlamalı akış](media-services-autogen-bitrate-ladder-with-mes.md) hazır.</span><span class="sxs-lookup"><span data-stu-id="a8d95-138">Specify toouse hello [Adaptive Streaming](media-services-autogen-bitrate-ladder-with-mes.md) preset.</span></span> 
* <span data-ttu-id="a8d95-139">Tek bir kodlama görev toohello işi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a8d95-139">Add a single encoding task toohello job.</span></span> 
* <span data-ttu-id="a8d95-140">Merhaba giriş belirtin kodlanmış varlık toobe.</span><span class="sxs-lookup"><span data-stu-id="a8d95-140">Specify hello input asset toobe encoded.</span></span>
* <span data-ttu-id="a8d95-141">Kodlanmış hello varlık içerecek bir çıkış varlığı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a8d95-141">Create an output asset that will contain hello encoded asset.</span></span>
* <span data-ttu-id="a8d95-142">Bir olay işleyicisi toocheck hello ilerleyişini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a8d95-142">Add an event handler toocheck hello job progress.</span></span>
* <span data-ttu-id="a8d95-143">Merhaba işi gönderin.</span><span class="sxs-lookup"><span data-stu-id="a8d95-143">Submit hello job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="a8d95-144">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a8d95-144">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="a8d95-145">Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="a8d95-145">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="a8d95-146">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8d95-146">Example</span></span> 

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderStandardSample
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

                    // Create a task with hello encoding details, using a string preset.
                    // In this case "Adaptive Streaming" preset is used.
                    ITask task = job.Tasks.AddNew("My encoding task",
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="a8d95-147">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="a8d95-147">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a8d95-148">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="a8d95-148">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="a8d95-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a8d95-149">Next steps</span></span>
<span data-ttu-id="a8d95-150">[Nasıl Medya Kodlayıcısı standart ile .NET kullanarak toogenerate küçük](media-services-dotnet-generate-thumbnail-with-mes.md)
[Media Services kodlama genel bakış](media-services-encode-asset.md)</span><span class="sxs-lookup"><span data-stu-id="a8d95-150">[How toogenerate thumbnail using Media Encoder Standard with .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[Media Services Encoding Overview](media-services-encode-asset.md)</span></span>

