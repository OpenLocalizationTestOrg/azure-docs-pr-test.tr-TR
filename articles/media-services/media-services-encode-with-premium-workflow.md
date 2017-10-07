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
# <a name="advanced-encoding-with-media-encoder-premium-workflow"></a>Medya Kodlayıcısı Premium akışıyla kodlama Gelişmiş
> [!NOTE]
> Bu konuda tartışılan Medya Kodlayıcısı Premium iş akışı medya işlemcisi Çin'de kullanılamaz.
>
>

Premium Kodlayıcı sorular için mepd adresindeki Microsoft.com e-posta.

## <a name="overview"></a>Genel Bakış
Microsoft Azure Media Services hello Tanıtımı **Medya Kodlayıcısı Premium iş akışı** medya işlemcisi. Bu işlemci teklifleri Gelişmiş özellikleri, premium isteğe bağlı iş akışları için kodlama.

Merhaba aşağıdaki konular anahat çok ilgili ayrıntıları**Medya Kodlayıcısı Premium iş akışı**:

* [Merhaba Medya Kodlayıcısı Premium iş akışı tarafından desteklenen biçimler](media-services-premium-workflow-encoder-formats.md) – anlatılmaktadır hello dosya biçimlerini ve tarafından desteklenen codec bileşenleri **Medya Kodlayıcısı Premium iş akışı**.
* [Genel bakış ve Azure karşılaştırma isteğe bağlı medya kodlayıcılar üzerine](media-services-encode-asset.md) karşılaştırır hello kodlama yeteneklerini **Medya Kodlayıcısı Premium iş akışı** ve **Medya Kodlayıcısı standart**.

Bu konuda gösterilir nasıl tooencode ile **Medya Kodlayıcısı Premium iş akışı** .NET kullanarak.

Merhaba görevlerde kodlama **Medya Kodlayıcısı Premium iş akışı** bir iş akışı dosyası adlı bir ayrı yapılandırma dosyası gerektirir. Bu dosyalar .workflow uzantısına sahiptir ve hello kullanılarak oluşturulan [iş akışı Tasarımcısı](media-services-workflow-designer.md) aracı.

Merhaba varsayılan iş akışı dosyalarını alabilir [burada](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows). Başlangıç klasörü de bu dosyaları hello açıklamasını içerir.

Merhaba iş akışı dosyalarını karşıya toobe tooyour Media Services hesabı bir varlık olarak gerekir ve bu varlık görev kodlama toohello geçirilmesi gerekir.

## <a name="create-and-configure-a-visual-studio-project"></a>Visual Studio projesi oluşturup yapılandırma

Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md). 

## <a name="encoding-example"></a>Kodlama örneği

Merhaba aşağıdaki örnekte gösterilmiştir nasıl tooencode ile **Medya Kodlayıcısı Premium iş akışı**.

Aşağıdaki adımları hello gerçekleştirilir:

1. Bir varlık oluşturun ve bir iş akışı dosyasını karşıya yükleyin.
2. Bir varlık oluşturun ve bir kaynak medya dosyasını karşıya yükleyin.
3. Merhaba "Medya Kodlayıcısı Premium iş akışı" medya işlemcisi alın.
4. Bir işi ve bir görev oluşturun.

    Çoğu durumda, hello yapılandırma dizesi hello görev için boştur (aşağıdaki örneğine hello ister). (Tootooset çalışma zamanı özellikleri dinamik olarak gerektirir) bazı Gelişmiş senaryolar vardır; bu durumda bir XML dizesi toohello kodlama görevi sağlar. Bu tür senaryoların örnekleri şunlardır: bir katmana, Dikiş, subtitling paralel veya sıralı medya oluşturma.
5. İki giriş varlıklar toohello görev ekleyin.

    1. 1 – hello iş akışı varlık.
    2. 2 – hello varlığı.

    >[!NOTE]
    >Merhaba iş akışı varlık toohello görev hello medya varlık önce eklenmesi gerekir.
   Bu görev için Hello yapılandırma dizesi boş olmalıdır.
   
6. Merhaba kodlama işi gönderin.

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

Premium Kodlayıcı sorular için mepd adresindeki Microsoft.com e-posta.

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
