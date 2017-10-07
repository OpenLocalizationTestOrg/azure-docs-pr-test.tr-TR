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
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a>Bir varlık Medya Kodlayıcısı .NET kullanarak standart ile kodlamak
Kodlama işleri hello en yaygın işlemleri Media Services biridir. Bir kodlama tooanother kodlama işleri tooconvert medya dosyaları oluşturun. Kodlarken, hello Media Services yerleşik medya kodlayıcı kullanabilirsiniz. Bir Media Services iş ortağı tarafından sağlanan bir kodlayıcı de kullanabilirsiniz; üçüncü taraf kodlayıcılar hello Azure Market kullanılabilir. 

Bu konuda gösterilmektedir nasıl toouse .NET tooencode varlıklarınızı ile Medya Kodlayıcısı standart (MES). Medya Kodlayıcısı standart yapılandırılmış açıklanan hello Kodlayıcı hazır birini kullanarak [burada](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

Tooalways Kaynak dosyalarınız Uyarlamalı bit hızlı MP4 kümesi kodlamak ve hello kullanarak hello kümesi toohello istenen biçimine dönüştür önerilen [dinamik paketleme](media-services-dynamic-packaging-overview.md). 

Çıkış varlığına depolama şifrelenmiş ise, varlık teslim ilkesini yapılandırmanız gerekir. Daha fazla bilgi için bkz: [varlık teslim ilkesini yapılandırma](media-services-dotnet-configure-asset-delivery-policy.md).

> [!NOTE]
> Bir çıkış dosyası içeren bir ad ile Merhaba ilk 32 karakteri MES üretir girdi dosyası adı hello. Merhaba ad hello hazır dosyasında belirtilen üzerinde temel alır. Örneğin, "dosya adı": "{Basename} _ {Index} {uzantısı}". {Basename} hello tarafından değiştirilir hello giriş dosyası adının ilk 32 karakteri.
> 
> 

### <a name="mes-formats"></a>MES biçimleri
[Biçimleri ve codec bileşenleri](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a>MES Ön ayarları
Medya Kodlayıcısı standart yapılandırılmış açıklanan hello Kodlayıcı hazır birini kullanarak [burada](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

### <a name="input-and-output-metadata"></a>Giriş ve çıkış meta verileri
Bir giriş varlık (veya varlıklar) MES kullanarak kodlarken bir çıkış varlığı edinme hello başarılı şekilde tamamlandığını, kodlama görev. Merhaba çıkış varlık, video, ses, küçük resimleri, bildirimi, kullandığınız hello kodlama hazır ayarına göre göre vb. içerir.

Merhaba çıkış varlığına hello giriş varlık hakkındaki meta verileri sahip bir dosya da içerir. Merhaba hello meta veri XML dosyası adına sahip biçimini izleyen hello: < asset_id > _metadata.xml (örneğin, 41114ad3-eb5e - 4 c 57-8 d 92-5354e2b7d4a4_metadata.xml), burada < asset_id > değeridir hello AssetID hello giriş varlık. Merhaba giriş bu meta veri XML Şeması açıklanan [burada](media-services-input-metadata-schema.md).

Merhaba çıkış varlığına hello çıkış varlık hakkındaki meta verileri sahip bir dosya da içerir. Merhaba hello meta veri XML dosyası adına sahip biçimini izleyen hello: < source_file_name > _manifest.xml (örneğin, BigBuckBunny_manifest.xml). XML açıklanmıştır Bu çıktı meta verileri Hello şeması [burada](media-services-output-metadata-schema.md).

Merhaba iki meta veri dosyalarının herhangi birini tooexamine istiyorsanız, bir SAS Bulucu oluşturmanız ve hello dosya tooyour yerel bilgisayara indirin. Toocreate bir SAS Bulucu ve yükleme dosyasını kullanarak hello medya hizmetleri nasıl üzerinde bir örnek bulabilirsiniz .NET SDK uzantıları.

## <a name="download-sample"></a>Örnek indirme
Alın ve gösteren bir örnek çalıştırın nasıl MES ile tooencode [burada](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).

## <a name="net-sample-code"></a>.NET örnek kod

Aşağıdaki kod örneğine hello görevleri aşağıdaki Media Services .NET SDK'sı tooperform hello kullanır:

* Bir kodlama işi oluşturun.
* Bir başvuru toohello Medya Kodlayıcısı standart Kodlayıcısı alın.
* Toouse hello belirtin [Uyarlamalı akış](media-services-autogen-bitrate-ladder-with-mes.md) hazır. 
* Tek bir kodlama görev toohello işi ekleyin. 
* Merhaba giriş belirtin kodlanmış varlık toobe.
* Kodlanmış hello varlık içerecek bir çıkış varlığı oluşturun.
* Bir olay işleyicisi toocheck hello ilerleyişini ekleyin.
* Merhaba işi gönderin.

#### <a name="create-and-configure-a-visual-studio-project"></a>Visual Studio projesi oluşturup yapılandırma

Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Örnek 

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

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Sonraki adımlar
[Nasıl Medya Kodlayıcısı standart ile .NET kullanarak toogenerate küçük](media-services-dotnet-generate-thumbnail-with-mes.md)
[Media Services kodlama genel bakış](media-services-encode-asset.md)

