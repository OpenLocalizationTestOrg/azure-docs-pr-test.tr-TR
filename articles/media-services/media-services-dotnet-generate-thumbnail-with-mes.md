---
title: "aaaHow toogenerate küçük resimleri Medya Kodlayıcısı standart .NET ile kullanma"
description: "Bu konuda gösterilmektedir nasıl toouse .NET tooencode bir varlık ve hello en küçük resimler oluşturma medya Kodlayıcı standart kullanarak aynı anda."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: b8dab73a-1d91-4b6d-9741-a92ad39fc3f7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: juliako
ms.openlocfilehash: 23d3e4d9bf64a688d45499c045f19d2792167990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-thumbnails-using-media-encoder-standard-with-net"></a><span data-ttu-id="c6e22-103">Nasıl toogenerate küçük resimleri Medya Kodlayıcısı standart .NET ile kullanma</span><span class="sxs-lookup"><span data-stu-id="c6e22-103">How toogenerate thumbnails using Media Encoder Standard with .NET</span></span>

<span data-ttu-id="c6e22-104">Video giriş öğesinden bir veya daha fazla küçük resimleri Medya Kodlayıcısı standart toogenerate kullanabilirsiniz [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), veya [BMP](https://en.wikipedia.org/wiki/BMP_file_format) görüntü dosyası biçimlerini.</span><span class="sxs-lookup"><span data-stu-id="c6e22-104">You can use Media Encoder Standard toogenerate one or more thumbnails from your input video in [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), or [BMP](https://en.wikipedia.org/wiki/BMP_file_format) image file formats.</span></span> <span data-ttu-id="c6e22-105">Yalnızca görüntü üretmek görevler gönderebilir veya kodlamalı küçük resim oluşturma birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c6e22-105">You can submit Tasks that produce only images, or you can combine thumbnail generation with encoding.</span></span> <span data-ttu-id="c6e22-106">Bu konu, bu tür senaryoları için birkaç örnek XML ve JSON küçük resim hazır sağlar.</span><span class="sxs-lookup"><span data-stu-id="c6e22-106">This topic provides a few sample XML and JSON thumbnail presets for such scenarios.</span></span> <span data-ttu-id="c6e22-107">Hello konunun Hello sonunda, var olan bir [örnek koduna](#code_sample) nasıl toouse hello Media Services .NET SDK'sı tooaccomplish hello kodlama görev gösterir.</span><span class="sxs-lookup"><span data-stu-id="c6e22-107">At hello end of hello topic, there is a [sample code](#code_sample) that shows how toouse hello Media Services .NET SDK tooaccomplish hello encoding task.</span></span>

<span data-ttu-id="c6e22-108">Örnek hazır kullanılan hello öğeleri hakkında daha fazla ayrıntı için gözden geçirmeniz gereken [Medya Kodlayıcısı standart şema](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="c6e22-108">For more details on hello elements that are used in sample presets, you should review [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>

<span data-ttu-id="c6e22-109">Tooreview hello emin olun [konuları](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) bölümü.</span><span class="sxs-lookup"><span data-stu-id="c6e22-109">Make sure tooreview hello [Considerations](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) section.</span></span>

## <a name="example--single-png-file"></a><span data-ttu-id="c6e22-110">Örnek – tek bir PNG dosyası</span><span class="sxs-lookup"><span data-stu-id="c6e22-110">Example – single PNG file</span></span>

<span data-ttu-id="c6e22-111">JSON aşağıdaki hello ve XML hazır, tek bir çıktı PNG dosya hello dışında ilk birkaç kullanılan tooproduce olabilir burada hello Kodlayıcı kılar "ilginç" Çerçeve bulma sırasında bir en yüksek çaba girişimi hello giriş video saniye.</span><span class="sxs-lookup"><span data-stu-id="c6e22-111">hello following JSON and XML preset can be used tooproduce a single output PNG file out of hello first few seconds of hello input video, where hello encoder makes a best-effort attempt at finding an “interesting” frame.</span></span> <span data-ttu-id="c6e22-112">Merhaba çıktı görüntü boyutları too100%, bunlar hello video boyutlarını hello giriş eşleşir anlamı ayarlanan unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c6e22-112">Note that hello output image dimensions have been set too100%, meaning these will match hello dimensions of hello input video.</span></span> <span data-ttu-id="c6e22-113">Ayrıca nasıl "Çıktı" hello "Format" ayarında gerekli Not "PngLayers" Merhaba "Codec bileşenleri" bölümünde toomatch hello kullanımı.</span><span class="sxs-lookup"><span data-stu-id="c6e22-113">Note also how hello “Format” setting in “Outputs” is required toomatch hello use of “PngLayers” in hello “Codecs” section.</span></span> 

### <a name="json-preset"></a><span data-ttu-id="c6e22-114">JSON hazır</span><span class="sxs-lookup"><span data-stu-id="c6e22-114">JSON preset</span></span>

    {
      "Version": 1.0,
      "Codecs": [
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": "100%",
              "Height": "100%"
            }
          ],
          "Start": "{Best}",
          "Type": "PngImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        }
      ]
    }
    
### <a name="xml-preset"></a><span data-ttu-id="c6e22-115">XML hazır</span><span class="sxs-lookup"><span data-stu-id="c6e22-115">XML preset</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <PngImage Start="{Best}">
          <PngLayers>
            <PngLayer>
              <Width>100%</Width>
              <Height>100%</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="example--a-series-of-jpeg-images"></a><span data-ttu-id="c6e22-116">Örnek – bir dizi JPEG görüntüleri</span><span class="sxs-lookup"><span data-stu-id="c6e22-116">Example – a series of JPEG images</span></span>

<span data-ttu-id="c6e22-117">JSON aşağıdaki hello ve XML hazır kullanılan tooproduce zaman damgaları % 5, 10 görüntülere bir dizi olabilir % 15,..., burada hello görüntü boyutu, belirtilen toobe bir video girişi, hello Çeyrek hello Giriş zaman çizelgesi % 95.</span><span class="sxs-lookup"><span data-stu-id="c6e22-117">hello following JSON and XML preset can be used tooproduce a set of 10 images at timestamps of 5%, 15%, …, 95% of hello input timeline, where hello image size is specified toobe one quarter that of hello input video.</span></span>

### <a name="json-preset"></a><span data-ttu-id="c6e22-118">JSON hazır</span><span class="sxs-lookup"><span data-stu-id="c6e22-118">JSON preset</span></span>

    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "25%",
              "Height": "25%"
            }
          ],
          "Start": "5%",
          "Step": "1",
          "Range": "1",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        }
      ]
    }

### <a name="xml-preset"></a><span data-ttu-id="c6e22-119">XML hazır</span><span class="sxs-lookup"><span data-stu-id="c6e22-119">XML preset</span></span>
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <JpgImage Start="5%" Step="10%" Range="96%">
          <JpgLayers>
            <JpgLayer>
              <Width>25%</Width>
              <Height>25%</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="example--one-image-at-a-specific-timestamp"></a><span data-ttu-id="c6e22-120">Örnek – belirli bir zaman damgası konumundaki bir görüntüsü</span><span class="sxs-lookup"><span data-stu-id="c6e22-120">Example – one image at a specific timestamp</span></span>

<span data-ttu-id="c6e22-121">JSON ve XML hazır aşağıdaki hello hello tek bir JPEG görüntüsüne 30 saniye işaretlemek hello giriş video kullanılan tooproduce olabilir.</span><span class="sxs-lookup"><span data-stu-id="c6e22-121">hello following JSON and XML preset can be used tooproduce a single JPEG image at hello 30 second mark of hello input video.</span></span> <span data-ttu-id="c6e22-122">Bu hazır hello giriş toobe süresi 30 saniyeden fazla bekliyor (başka hello işi başarısız olur).</span><span class="sxs-lookup"><span data-stu-id="c6e22-122">This preset expects hello input toobe more than 30 seconds in duration (else hello job will fail).</span></span>

### <a name="json-preset"></a><span data-ttu-id="c6e22-123">JSON hazır</span><span class="sxs-lookup"><span data-stu-id="c6e22-123">JSON preset</span></span>

    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "25%",
              "Height": "25%"
            }
          ],
          "Start": "00:00:30",
          "Step": "1",
          "Range": "1",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        }
      ]
    }
    
### <a name="xml-preset"></a><span data-ttu-id="c6e22-124">XML hazır</span><span class="sxs-lookup"><span data-stu-id="c6e22-124">XML preset</span></span>
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <JpgImage Start="00:00:30" Step="00:00:02" Range="00:00:01">
          <JpgLayers>
            <JpgLayer>
              <Width>25%</Width>
              <Height>25%</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <span data-ttu-id="c6e22-125"><a id="code_sample"></a>Örnek – videoyu kodlamak ve küçük resim oluşturma</span><span class="sxs-lookup"><span data-stu-id="c6e22-125"><a id="code_sample"></a>Example – encode video and generate thumbnail</span></span>

<span data-ttu-id="c6e22-126">Aşağıdaki kod örneğine hello görevleri aşağıdaki Media Services .NET SDK'sı tooperform hello kullanır:</span><span class="sxs-lookup"><span data-stu-id="c6e22-126">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

* <span data-ttu-id="c6e22-127">Bir kodlama işi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c6e22-127">Create an encoding job.</span></span>
* <span data-ttu-id="c6e22-128">Bir başvuru toohello Medya Kodlayıcısı standart Kodlayıcısı alın.</span><span class="sxs-lookup"><span data-stu-id="c6e22-128">Get a reference toohello Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="c6e22-129">Yük hello önceden [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) veya [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) içeren yanı sıra toogenerate küçük resimleri gerekli bilgiler önceden hello kodlama.</span><span class="sxs-lookup"><span data-stu-id="c6e22-129">Load hello preset [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) that contain hello encoding preset as well as information needed toogenerate thumbnails.</span></span> <span data-ttu-id="c6e22-130">Bu kaydedebilirsiniz [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) veya [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) aşağıdaki kodu tooload hello dosyasına bir dosya ve kullanım hello içinde.</span><span class="sxs-lookup"><span data-stu-id="c6e22-130">You can save this  [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) in a file and use hello following code tooload hello file.</span></span>
  
        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(fileName);  
* <span data-ttu-id="c6e22-131">Tek bir kodlama görev toohello işi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c6e22-131">Add a single encoding task toohello job.</span></span> 
* <span data-ttu-id="c6e22-132">Merhaba giriş belirtin kodlanmış varlık toobe.</span><span class="sxs-lookup"><span data-stu-id="c6e22-132">Specify hello input asset toobe encoded.</span></span>
* <span data-ttu-id="c6e22-133">Kodlanmış hello varlık içerecek bir çıkış varlığı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c6e22-133">Create an output asset that will contain hello encoded asset.</span></span>
* <span data-ttu-id="c6e22-134">Bir olay işleyicisi toocheck hello ilerleyişini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c6e22-134">Add an event handler toocheck hello job progress.</span></span>
* <span data-ttu-id="c6e22-135">Merhaba işi gönderin.</span><span class="sxs-lookup"><span data-stu-id="c6e22-135">Submit hello job.</span></span>

<span data-ttu-id="c6e22-136">Merhaba bkz [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md) konu konusunda yönergeler için geliştirme ortamınızı tooset.</span><span class="sxs-lookup"><span data-stu-id="c6e22-136">See hello [Media Services development with .NET](media-services-dotnet-how-to-use.md) topic for directions on how tooset up your dev environment.</span></span>

        using System;
        using System.Configuration;
        using System.IO;
        using System.Linq;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;

        namespace EncodeAndGenerateThumbnails
        {
        class Program
        {
            // Read values from hello App.config file.
            private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            private static CloudMediaContext _context = null;

            private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

            private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

            static void Main(string[] args)
            {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate hello thumbnails.
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

            // Load hello XML (or JSON) from hello local file.
            string configuration = File.ReadAllText("ThumbnailPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
                processor,
                configuration,
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

## <span data-ttu-id="c6e22-137"><a id="json"></a>Küçük resim JSON hazır</span><span class="sxs-lookup"><span data-stu-id="c6e22-137"><a id="json"></a>Thumbnail JSON preset</span></span>
<span data-ttu-id="c6e22-138">Şeması hakkında daha fazla bilgi için bkz: [bu](https://msdn.microsoft.com/library/mt269962.aspx) konu.</span><span class="sxs-lookup"><span data-stu-id="c6e22-138">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>

    {
      "Version": 1.0,
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": "true",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 4500,
              "MaxBitrate": 4500,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "ReferenceFrames": 3,
              "EntropyMode": "Cabac",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
    
            }
          ],
          "Type": "H264Video"
        },
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "100%",
              "Height": "100%"
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        },
        {
          "FileName": "{Basename}_{Resolution}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <span data-ttu-id="c6e22-139"><a id="xml"></a>Küçük resim XML hazır</span><span class="sxs-lookup"><span data-stu-id="c6e22-139"><a id="xml"></a>Thumbnail XML preset</span></span>
<span data-ttu-id="c6e22-140">Şeması hakkında daha fazla bilgi için bkz: [bu](https://msdn.microsoft.com/library/mt269962.aspx) konu.</span><span class="sxs-lookup"><span data-stu-id="c6e22-140">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <SceneChangeDetection>true</SceneChangeDetection>
          <H264Layers>
            <H264Layer>
              <Bitrate>4500</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>4500</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
        <JpgImage Start="{Best}">
          <JpgLayers>
            <JpgLayer>
              <Width>100%</Width>
              <Height>100%/Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Resolution}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="considerations"></a><span data-ttu-id="c6e22-141">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="c6e22-141">Considerations</span></span>
<span data-ttu-id="c6e22-142">ilgili önemli noktalar aşağıdaki hello Uygula:</span><span class="sxs-lookup"><span data-stu-id="c6e22-142">hello following considerations apply:</span></span>

* <span data-ttu-id="c6e22-143">Merhaba kullanımına açık zaman damgaları Başlat/adım/aralık en az 1 dakika uzun bu hello giriş kaynağı olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="c6e22-143">hello use of explicit timestamps for Start/Step/Range assumes that hello input source is at least 1 minute long.</span></span>
* <span data-ttu-id="c6e22-144">Başlangıç, adım ve öznitelikleri dize aralığı Png/jpg/BmpImage öğeleri sahip – bu olarak yorumlanacak:</span><span class="sxs-lookup"><span data-stu-id="c6e22-144">Jpg/Png/BmpImage elements have Start, Step and Range string attributes – these can be interpreted as:</span></span>
  
  * <span data-ttu-id="c6e22-145">Negatif olmayan tamsayılar ör olmaları durumunda çerçeve numarası.</span><span class="sxs-lookup"><span data-stu-id="c6e22-145">Frame Number if they are non-negative integers, eg.</span></span> <span data-ttu-id="c6e22-146">"Başlat": "120",</span><span class="sxs-lookup"><span data-stu-id="c6e22-146">"Start": "120",</span></span>
  * <span data-ttu-id="c6e22-147">% Sonekine olarak ör ifade, göreli toosource süresi.</span><span class="sxs-lookup"><span data-stu-id="c6e22-147">Relative toosource duration if expressed as %-suffixed, eg.</span></span> <span data-ttu-id="c6e22-148">"Başlat": "% 15", veya</span><span class="sxs-lookup"><span data-stu-id="c6e22-148">"Start": "15%", OR</span></span>
  * <span data-ttu-id="c6e22-149">Ss: dd: ifade edilen, zaman damgası...</span><span class="sxs-lookup"><span data-stu-id="c6e22-149">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="c6e22-150">biçimi.</span><span class="sxs-lookup"><span data-stu-id="c6e22-150">format.</span></span> <span data-ttu-id="c6e22-151">Ör.</span><span class="sxs-lookup"><span data-stu-id="c6e22-151">Eg.</span></span> <span data-ttu-id="c6e22-152">"Başlat": "00: 01:00"</span><span class="sxs-lookup"><span data-stu-id="c6e22-152">"Start" : "00:01:00"</span></span>
    
    <span data-ttu-id="c6e22-153">Karışık ve yazarken gösterimler Lütfen eşleşmesi.</span><span class="sxs-lookup"><span data-stu-id="c6e22-153">You can mix and match notations as you please.</span></span>
    
    <span data-ttu-id="c6e22-154">Ayrıca, başlangıç özel makrosu de destekler: {, hangi toodetermine hello ilk "ilginç" Çerçeve hello içeriğin Not çalışır en iyi}: (adım ve aralığı dikkate alınmaz başlangıç çok ayarlandığında {en iyi})</span><span class="sxs-lookup"><span data-stu-id="c6e22-154">Additionally, Start also supports a special Macro:{Best}, which attempts toodetermine hello first “interesting” frame of hello content NOTE: (Step and Range are ignored when Start is set too{Best})</span></span>
  * <span data-ttu-id="c6e22-155">Varsayılan: Başlat: {en iyi}</span><span class="sxs-lookup"><span data-stu-id="c6e22-155">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="c6e22-156">Çıktı biçimi açıkça her resim biçimi için sağlanan toobe gerekiyor: Png/Jpg/BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="c6e22-156">Output format needs toobe explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="c6e22-157">Varsa, MES JpgVideo tooJpgFormat vb. ile eşleşir.</span><span class="sxs-lookup"><span data-stu-id="c6e22-157">When present, MES will match JpgVideo tooJpgFormat and so on.</span></span> <span data-ttu-id="c6e22-158">Yeni bir görüntü codec belirli makrosu OutputFormat sunar: {, hangi toobe mevcut (bir kez ve yalnızca bir kez) gereken görüntü Çıkış biçimleri için dizin}.</span><span class="sxs-lookup"><span data-stu-id="c6e22-158">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs toobe present (once and only once) for image output formats.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6e22-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c6e22-159">Next steps</span></span>

<span data-ttu-id="c6e22-160">Merhaba denetleyebilirsiniz [iş ilerleme](media-services-check-job-progress.md) sırasında hello kodlama işinin bekliyor.</span><span class="sxs-lookup"><span data-stu-id="c6e22-160">You can check hello [job progress](media-services-check-job-progress.md) while hello encoding job is pending.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="c6e22-161">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="c6e22-161">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c6e22-162">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="c6e22-162">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="c6e22-163">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="c6e22-163">See Also</span></span>
[<span data-ttu-id="c6e22-164">Media Services kodlama a genel bakış</span><span class="sxs-lookup"><span data-stu-id="c6e22-164">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

