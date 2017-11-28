---
title: "Media Encoder Standard ve .NET kullanarak küçük resim oluşturma"
description: "Bu konu, .NET bir varlık kodlama ve küçük resimleri medya Kodlayıcı standart kullanarak aynı anda oluşturmak için nasıl kullanılacağını gösterir."
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
ms.openlocfilehash: 89d15cbdf71a140e78f34e07ff208776b7d4cab3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-generate-thumbnails-using-media-encoder-standard-with-net"></a><span data-ttu-id="e312b-103">Media Encoder Standard ve .NET kullanarak küçük resim oluşturma</span><span class="sxs-lookup"><span data-stu-id="e312b-103">How to generate thumbnails using Media Encoder Standard with .NET</span></span>

<span data-ttu-id="e312b-104">Medya Kodlayıcısı standart bir veya daha fazla küçük resimleri girişinizi video oluşturmak için kullanabileceğiniz [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), veya [BMP](https://en.wikipedia.org/wiki/BMP_file_format) görüntü dosyası biçimlerini.</span><span class="sxs-lookup"><span data-stu-id="e312b-104">You can use Media Encoder Standard to generate one or more thumbnails from your input video in [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), or [BMP](https://en.wikipedia.org/wiki/BMP_file_format) image file formats.</span></span> <span data-ttu-id="e312b-105">Yalnızca görüntü üretmek görevler gönderebilir veya kodlamalı küçük resim oluşturma birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e312b-105">You can submit Tasks that produce only images, or you can combine thumbnail generation with encoding.</span></span> <span data-ttu-id="e312b-106">Bu konu, bu tür senaryoları için birkaç örnek XML ve JSON küçük resim hazır sağlar.</span><span class="sxs-lookup"><span data-stu-id="e312b-106">This topic provides a few sample XML and JSON thumbnail presets for such scenarios.</span></span> <span data-ttu-id="e312b-107">Konunun sonunda yoktur bir [örnek koduna](#code_sample) Media Services .NET SDK'sı kodlama görevi gerçekleştirmek için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e312b-107">At the end of the topic, there is a [sample code](#code_sample) that shows how to use the Media Services .NET SDK to accomplish the encoding task.</span></span>

<span data-ttu-id="e312b-108">Örnek hazır kullanılan öğeleri hakkında daha fazla ayrıntı için gözden geçirmeniz gereken [Medya Kodlayıcısı standart şema](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="e312b-108">For more details on the elements that are used in sample presets, you should review [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>

<span data-ttu-id="e312b-109">Gözden geçirdiğinizden emin olun [konuları](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) bölümü.</span><span class="sxs-lookup"><span data-stu-id="e312b-109">Make sure to review the [Considerations](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) section.</span></span>

## <a name="example--single-png-file"></a><span data-ttu-id="e312b-110">Örnek – tek bir PNG dosyası</span><span class="sxs-lookup"><span data-stu-id="e312b-110">Example – single PNG file</span></span>

<span data-ttu-id="e312b-111">Aşağıdaki JSON ve XML hazır burada Kodlayıcı "ilginç" Çerçeve bulma sırasında bir en yüksek çaba girişiminde bulunur tek bir çıktı PNG dosya video giriş ilk birkaç saniye dışında oluşturmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e312b-111">The following JSON and XML preset can be used to produce a single output PNG file out of the first few seconds of the input video, where the encoder makes a best-effort attempt at finding an “interesting” frame.</span></span> <span data-ttu-id="e312b-112">Bunlar anlamı % 100'e, çıktı görüntü boyutları ayarlanan Not video giriş boyutlarını eşleşir.</span><span class="sxs-lookup"><span data-stu-id="e312b-112">Note that the output image dimensions have been set to 100%, meaning these will match the dimensions of the input video.</span></span> <span data-ttu-id="e312b-113">Ayrıca "Çıktı" içindeki "Format" ayarı "Codec bileşenleri" bölümündeki "PngLayers" kullanımını eşleşecek şekilde nasıl gerekli unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e312b-113">Note also how the “Format” setting in “Outputs” is required to match the use of “PngLayers” in the “Codecs” section.</span></span> 

### <a name="json-preset"></a><span data-ttu-id="e312b-114">JSON hazır</span><span class="sxs-lookup"><span data-stu-id="e312b-114">JSON preset</span></span>

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
    
### <a name="xml-preset"></a><span data-ttu-id="e312b-115">XML hazır</span><span class="sxs-lookup"><span data-stu-id="e312b-115">XML preset</span></span>

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

## <a name="example--a-series-of-jpeg-images"></a><span data-ttu-id="e312b-116">Örnek – bir dizi JPEG görüntüleri</span><span class="sxs-lookup"><span data-stu-id="e312b-116">Example – a series of JPEG images</span></span>

<span data-ttu-id="e312b-117">Zaman damgaları 5 10 görüntülere kümesi oluşturmak için aşağıdaki JSON ve XML hazır kullanılabilir %, % 15,..., burada görüntü boyutu belirtildiği için giriş çizelgesinin % 95 quarter, video girişi.</span><span class="sxs-lookup"><span data-stu-id="e312b-117">The following JSON and XML preset can be used to produce a set of 10 images at timestamps of 5%, 15%, …, 95% of the input timeline, where the image size is specified to be one quarter that of the input video.</span></span>

### <a name="json-preset"></a><span data-ttu-id="e312b-118">JSON hazır</span><span class="sxs-lookup"><span data-stu-id="e312b-118">JSON preset</span></span>

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

### <a name="xml-preset"></a><span data-ttu-id="e312b-119">XML hazır</span><span class="sxs-lookup"><span data-stu-id="e312b-119">XML preset</span></span>
    
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

## <a name="example--one-image-at-a-specific-timestamp"></a><span data-ttu-id="e312b-120">Örnek – belirli bir zaman damgası konumundaki bir görüntüsü</span><span class="sxs-lookup"><span data-stu-id="e312b-120">Example – one image at a specific timestamp</span></span>

<span data-ttu-id="e312b-121">Aşağıdaki JSON ve XML hazır giriş videonun 30 ikinci işaretten tek bir JPEG görüntüsü oluşturmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e312b-121">The following JSON and XML preset can be used to produce a single JPEG image at the 30 second mark of the input video.</span></span> <span data-ttu-id="e312b-122">Bu hazır süresi 30 saniyeden fazla girişin olmasını bekliyor (else işi başarısız olur).</span><span class="sxs-lookup"><span data-stu-id="e312b-122">This preset expects the input to be more than 30 seconds in duration (else the job will fail).</span></span>

### <a name="json-preset"></a><span data-ttu-id="e312b-123">JSON hazır</span><span class="sxs-lookup"><span data-stu-id="e312b-123">JSON preset</span></span>

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
    
### <a name="xml-preset"></a><span data-ttu-id="e312b-124">XML hazır</span><span class="sxs-lookup"><span data-stu-id="e312b-124">XML preset</span></span>
    
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

## <span data-ttu-id="e312b-125"><a id="code_sample"></a>Örnek – videoyu kodlamak ve küçük resim oluşturma</span><span class="sxs-lookup"><span data-stu-id="e312b-125"><a id="code_sample"></a>Example – encode video and generate thumbnail</span></span>

<span data-ttu-id="e312b-126">Aşağıdaki kod örneği, aşağıdaki görevleri gerçekleştirmek için Media Services .NET SDK'sını kullanır:</span><span class="sxs-lookup"><span data-stu-id="e312b-126">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

* <span data-ttu-id="e312b-127">Bir kodlama işi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e312b-127">Create an encoding job.</span></span>
* <span data-ttu-id="e312b-128">Medya Kodlayıcısı standart Kodlayıcı başvuru alın.</span><span class="sxs-lookup"><span data-stu-id="e312b-128">Get a reference to the Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="e312b-129">Önceden ayarlanmış yük [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) veya [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) içeren küçük resimleri oluşturmak için gereken bilgileri yanı sıra önceden kodlama.</span><span class="sxs-lookup"><span data-stu-id="e312b-129">Load the preset [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) that contain the encoding preset as well as information needed to generate thumbnails.</span></span> <span data-ttu-id="e312b-130">Bu kaydedebilirsiniz [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) veya [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) bir dosya ve Kullan dosyayı yüklemek için aşağıdaki kod.</span><span class="sxs-lookup"><span data-stu-id="e312b-130">You can save this  [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) in a file and use the following code to load the file.</span></span>
  
        // Load the XML (or JSON) from the local file.
        string configuration = File.ReadAllText(fileName);  
* <span data-ttu-id="e312b-131">Tek bir kodlama görev projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e312b-131">Add a single encoding task to the job.</span></span> 
* <span data-ttu-id="e312b-132">Kodlanacak giriş varlık belirtin.</span><span class="sxs-lookup"><span data-stu-id="e312b-132">Specify the input asset to be encoded.</span></span>
* <span data-ttu-id="e312b-133">Kodlanmış varlık içerecek bir çıkış varlığı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e312b-133">Create an output asset that will contain the encoded asset.</span></span>
* <span data-ttu-id="e312b-134">İş ilerleme durumunu denetlemek için olay işleyici ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e312b-134">Add an event handler to check the job progress.</span></span>
* <span data-ttu-id="e312b-135">İşi göndermek.</span><span class="sxs-lookup"><span data-stu-id="e312b-135">Submit the job.</span></span>

<span data-ttu-id="e312b-136">Bkz: [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md) konu geliştirme ortamınızı ayarlama konusunda yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="e312b-136">See the [Media Services development with .NET](media-services-dotnet-how-to-use.md) topic for directions on how to set up your dev environment.</span></span>

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
            // Read values from the App.config file.
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

            // Encode and generate the thumbnails.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
            }

            static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
            {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Load the XML (or JSON) from the local file.
            string configuration = File.ReadAllText("ThumbnailPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
                processor,
                configuration,
                TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
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

## <span data-ttu-id="e312b-137"><a id="json"></a>Küçük resim JSON hazır</span><span class="sxs-lookup"><span data-stu-id="e312b-137"><a id="json"></a>Thumbnail JSON preset</span></span>
<span data-ttu-id="e312b-138">Şeması hakkında daha fazla bilgi için bkz: [bu](https://msdn.microsoft.com/library/mt269962.aspx) konu.</span><span class="sxs-lookup"><span data-stu-id="e312b-138">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>

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

## <span data-ttu-id="e312b-139"><a id="xml"></a>Küçük resim XML hazır</span><span class="sxs-lookup"><span data-stu-id="e312b-139"><a id="xml"></a>Thumbnail XML preset</span></span>
<span data-ttu-id="e312b-140">Şeması hakkında daha fazla bilgi için bkz: [bu](https://msdn.microsoft.com/library/mt269962.aspx) konu.</span><span class="sxs-lookup"><span data-stu-id="e312b-140">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>
    
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

## <a name="considerations"></a><span data-ttu-id="e312b-141">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="e312b-141">Considerations</span></span>
<span data-ttu-id="e312b-142">Aşağıdaki maddeler geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="e312b-142">The following considerations apply:</span></span>

* <span data-ttu-id="e312b-143">Başlangıç/adım/aralığı için açık zaman damgaları kullanımını giriş kaynağı en az 1 dakika uzun olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="e312b-143">The use of explicit timestamps for Start/Step/Range assumes that the input source is at least 1 minute long.</span></span>
* <span data-ttu-id="e312b-144">Başlangıç, adım ve öznitelikleri dize aralığı Png/jpg/BmpImage öğeleri sahip – bu olarak yorumlanacak:</span><span class="sxs-lookup"><span data-stu-id="e312b-144">Jpg/Png/BmpImage elements have Start, Step and Range string attributes – these can be interpreted as:</span></span>
  
  * <span data-ttu-id="e312b-145">Negatif olmayan tamsayılar ör olmaları durumunda çerçeve numarası.</span><span class="sxs-lookup"><span data-stu-id="e312b-145">Frame Number if they are non-negative integers, eg.</span></span> <span data-ttu-id="e312b-146">"Başlat": "120",</span><span class="sxs-lookup"><span data-stu-id="e312b-146">"Start": "120",</span></span>
  * <span data-ttu-id="e312b-147">Göreli % sonekine olarak ör ifade, kaynak süresi.</span><span class="sxs-lookup"><span data-stu-id="e312b-147">Relative to source duration if expressed as %-suffixed, eg.</span></span> <span data-ttu-id="e312b-148">"Başlat": "% 15", veya</span><span class="sxs-lookup"><span data-stu-id="e312b-148">"Start": "15%", OR</span></span>
  * <span data-ttu-id="e312b-149">Ss: dd: ifade edilen, zaman damgası...</span><span class="sxs-lookup"><span data-stu-id="e312b-149">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="e312b-150">biçimi.</span><span class="sxs-lookup"><span data-stu-id="e312b-150">format.</span></span> <span data-ttu-id="e312b-151">Ör.</span><span class="sxs-lookup"><span data-stu-id="e312b-151">Eg.</span></span> <span data-ttu-id="e312b-152">"Başlat": "00: 01:00"</span><span class="sxs-lookup"><span data-stu-id="e312b-152">"Start" : "00:01:00"</span></span>
    
    <span data-ttu-id="e312b-153">Karışık ve yazarken gösterimler Lütfen eşleşmesi.</span><span class="sxs-lookup"><span data-stu-id="e312b-153">You can mix and match notations as you please.</span></span>
    
    <span data-ttu-id="e312b-154">Ayrıca, başlangıç özel makrosu de destekler: {, hangi içerik Not ilk "ilginç" çerçevesi belirlemeyi dener en iyi}: (adım ve aralık yok sayılır başlangıç {iyi} olarak ayarlandığında geçerlidir)</span><span class="sxs-lookup"><span data-stu-id="e312b-154">Additionally, Start also supports a special Macro:{Best}, which attempts to determine the first “interesting” frame of the content NOTE: (Step and Range are ignored when Start is set to {Best})</span></span>
  * <span data-ttu-id="e312b-155">Varsayılan: Başlat: {en iyi}</span><span class="sxs-lookup"><span data-stu-id="e312b-155">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="e312b-156">Çıktı biçimi her resim biçimi için açıkça sağlanması gerekiyor: Png/Jpg/BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="e312b-156">Output format needs to be explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="e312b-157">Varsa, MES JpgFormat JpgVideo vb. ile eşleşir.</span><span class="sxs-lookup"><span data-stu-id="e312b-157">When present, MES will match JpgVideo to JpgFormat and so on.</span></span> <span data-ttu-id="e312b-158">Yeni bir görüntü codec belirli makrosu OutputFormat sunar: {Index} olması gerekiyor hangi sunmak (bir kez ve yalnızca bir kez) görüntü Çıkış biçimleri.</span><span class="sxs-lookup"><span data-stu-id="e312b-158">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs to be present (once and only once) for image output formats.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e312b-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e312b-159">Next steps</span></span>

<span data-ttu-id="e312b-160">Kontrol edebilirsiniz [iş ilerleme](media-services-check-job-progress.md) kodlama işinin beklemedeyken.</span><span class="sxs-lookup"><span data-stu-id="e312b-160">You can check the [job progress](media-services-check-job-progress.md) while the encoding job is pending.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="e312b-161">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="e312b-161">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e312b-162">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="e312b-162">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="e312b-163">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="e312b-163">See Also</span></span>
[<span data-ttu-id="e312b-164">Media Services kodlama a genel bakış</span><span class="sxs-lookup"><span data-stu-id="e312b-164">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

