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
# <a name="how-toogenerate-thumbnails-using-media-encoder-standard-with-net"></a>Nasıl toogenerate küçük resimleri Medya Kodlayıcısı standart .NET ile kullanma

Video giriş öğesinden bir veya daha fazla küçük resimleri Medya Kodlayıcısı standart toogenerate kullanabilirsiniz [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), veya [BMP](https://en.wikipedia.org/wiki/BMP_file_format) görüntü dosyası biçimlerini. Yalnızca görüntü üretmek görevler gönderebilir veya kodlamalı küçük resim oluşturma birleştirebilirsiniz. Bu konu, bu tür senaryoları için birkaç örnek XML ve JSON küçük resim hazır sağlar. Hello konunun Hello sonunda, var olan bir [örnek koduna](#code_sample) nasıl toouse hello Media Services .NET SDK'sı tooaccomplish hello kodlama görev gösterir.

Örnek hazır kullanılan hello öğeleri hakkında daha fazla ayrıntı için gözden geçirmeniz gereken [Medya Kodlayıcısı standart şema](media-services-mes-schema.md).

Tooreview hello emin olun [konuları](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) bölümü.

## <a name="example--single-png-file"></a>Örnek – tek bir PNG dosyası

JSON aşağıdaki hello ve XML hazır, tek bir çıktı PNG dosya hello dışında ilk birkaç kullanılan tooproduce olabilir burada hello Kodlayıcı kılar "ilginç" Çerçeve bulma sırasında bir en yüksek çaba girişimi hello giriş video saniye. Merhaba çıktı görüntü boyutları too100%, bunlar hello video boyutlarını hello giriş eşleşir anlamı ayarlanan unutmayın. Ayrıca nasıl "Çıktı" hello "Format" ayarında gerekli Not "PngLayers" Merhaba "Codec bileşenleri" bölümünde toomatch hello kullanımı. 

### <a name="json-preset"></a>JSON hazır

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
    
### <a name="xml-preset"></a>XML hazır

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

## <a name="example--a-series-of-jpeg-images"></a>Örnek – bir dizi JPEG görüntüleri

JSON aşağıdaki hello ve XML hazır kullanılan tooproduce zaman damgaları % 5, 10 görüntülere bir dizi olabilir % 15,..., burada hello görüntü boyutu, belirtilen toobe bir video girişi, hello Çeyrek hello Giriş zaman çizelgesi % 95.

### <a name="json-preset"></a>JSON hazır

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

### <a name="xml-preset"></a>XML hazır
    
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

## <a name="example--one-image-at-a-specific-timestamp"></a>Örnek – belirli bir zaman damgası konumundaki bir görüntüsü

JSON ve XML hazır aşağıdaki hello hello tek bir JPEG görüntüsüne 30 saniye işaretlemek hello giriş video kullanılan tooproduce olabilir. Bu hazır hello giriş toobe süresi 30 saniyeden fazla bekliyor (başka hello işi başarısız olur).

### <a name="json-preset"></a>JSON hazır

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
    
### <a name="xml-preset"></a>XML hazır
    
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

## <a id="code_sample"></a>Örnek – videoyu kodlamak ve küçük resim oluşturma

Aşağıdaki kod örneğine hello görevleri aşağıdaki Media Services .NET SDK'sı tooperform hello kullanır:

* Bir kodlama işi oluşturun.
* Bir başvuru toohello Medya Kodlayıcısı standart Kodlayıcısı alın.
* Yük hello önceden [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) veya [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) içeren yanı sıra toogenerate küçük resimleri gerekli bilgiler önceden hello kodlama. Bu kaydedebilirsiniz [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) veya [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) aşağıdaki kodu tooload hello dosyasına bir dosya ve kullanım hello içinde.
  
        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(fileName);  
* Tek bir kodlama görev toohello işi ekleyin. 
* Merhaba giriş belirtin kodlanmış varlık toobe.
* Kodlanmış hello varlık içerecek bir çıkış varlığı oluşturun.
* Bir olay işleyicisi toocheck hello ilerleyişini ekleyin.
* Merhaba işi gönderin.

Merhaba bkz [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md) konu konusunda yönergeler için geliştirme ortamınızı tooset.

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

## <a id="json"></a>Küçük resim JSON hazır
Şeması hakkında daha fazla bilgi için bkz: [bu](https://msdn.microsoft.com/library/mt269962.aspx) konu.

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

## <a id="xml"></a>Küçük resim XML hazır
Şeması hakkında daha fazla bilgi için bkz: [bu](https://msdn.microsoft.com/library/mt269962.aspx) konu.
    
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

## <a name="considerations"></a>Dikkat edilmesi gerekenler
ilgili önemli noktalar aşağıdaki hello Uygula:

* Merhaba kullanımına açık zaman damgaları Başlat/adım/aralık en az 1 dakika uzun bu hello giriş kaynağı olduğunu varsayar.
* Başlangıç, adım ve öznitelikleri dize aralığı Png/jpg/BmpImage öğeleri sahip – bu olarak yorumlanacak:
  
  * Negatif olmayan tamsayılar ör olmaları durumunda çerçeve numarası. "Başlat": "120",
  * % Sonekine olarak ör ifade, göreli toosource süresi. "Başlat": "% 15", veya
  * Ss: dd: ifade edilen, zaman damgası... biçimi. Ör. "Başlat": "00: 01:00"
    
    Karışık ve yazarken gösterimler Lütfen eşleşmesi.
    
    Ayrıca, başlangıç özel makrosu de destekler: {, hangi toodetermine hello ilk "ilginç" Çerçeve hello içeriğin Not çalışır en iyi}: (adım ve aralığı dikkate alınmaz başlangıç çok ayarlandığında {en iyi})
  * Varsayılan: Başlat: {en iyi}
* Çıktı biçimi açıkça her resim biçimi için sağlanan toobe gerekiyor: Png/Jpg/BmpFormat. Varsa, MES JpgVideo tooJpgFormat vb. ile eşleşir. Yeni bir görüntü codec belirli makrosu OutputFormat sunar: {, hangi toobe mevcut (bir kez ve yalnızca bir kez) gereken görüntü Çıkış biçimleri için dizin}.

## <a name="next-steps"></a>Sonraki adımlar

Merhaba denetleyebilirsiniz [iş ilerleme](media-services-check-job-progress.md) sırasında hello kodlama işinin bekliyor.

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Ayrıca Bkz.
[Media Services kodlama a genel bakış](media-services-encode-asset.md)

