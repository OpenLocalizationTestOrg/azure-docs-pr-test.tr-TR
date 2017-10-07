---
title: "aaaPerform Gelişmiş MES hazır özelleştirerek kodlama | Microsoft Docs"
description: "Bu konu, Medya Kodlayıcısı standart görev hazır özelleştirerek kodlama tooperform nasıl Gelişmiş gösterir."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 2a4ade25-e600-4bce-a66e-e29cf4a38369
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: juliako
ms.openlocfilehash: 9caa68fafacaf51f91f0554c5bafe491928d8c77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-encoding-by-customizing-mes-presets"></a>Gelişmiş kodlama MES hazır ayarlarını özelleştirerek gerçekleştirin 

## <a name="overview"></a>Genel Bakış

Bu konuda nasıl toocustomize Medya Kodlayıcısı standart hazır ayarları gösterilmektedir. Merhaba [Medya Kodlayıcısı özel hazır ayarları kullanarak standart ile kodlama](media-services-custom-mes-presets-with-dotnet.md) konu, nasıl bir kodlama toouse .NET toocreate görev ve bu görevi yürüten bir işi gösterir. Bir hazır tedarik hello özel hazır toohello kodlama görev özelleştirildikten sonra. 

>[!NOTE]
>Bir XML hazır kullanıyorsanız, XML örneklerinde aşağıda gösterildiği gibi öğeleri emin toopreserve hello sırasını olun (örneğin, KeyFrameInterval SceneChangeDetection gelmelidir).
>

Bu konuda, kodlama görevleri aşağıdaki hello gerçekleştirmek hello özel hazır gösterilmiştir.

## <a name="support-for-relative-sizes"></a>Göreli boyutları için destek

Küçük resimleri oluştururken, gereksinim tooalways çıkış genişlik ve yükseklik piksel cinsinden belirtin. [% 1,..., % 100] hello aralıktaki yüzde belirtebilirsiniz.

### <a name="json-preset"></a>JSON hazır
    "Width": "100%",
    "Height": "100%"

### <a name="xml-preset"></a>XML hazır
    <Width>100%</Width>
    <Height>100%</Height>

## <a id="thumbnails"></a>Küçük resimler oluşturma

Bu bölümde gösterilmiştir nasıl toocustomize küçük resim oluşturur hazır. Merhaba aşağıda tanımlanan hazır tooencode istediğiniz bilgi dosyanızı yanı sıra toogenerate küçük resimleri gerekli bilgiler içerir. Merhaba MES hazır belgelenen hiçbirini uygulayabileceğiniz [bu](media-services-mes-presets-overview.md) bölümünde ve küçük resim oluşturur kodu ekleyin.  

> [!NOTE]
> Merhaba **SceneChangeDetection** hazır aşağıdaki hello ayarında yalnızca ayarlanabilir tootrue tooa tek bit hızlı video kodlama durumunda. Tooa Çoklu bit hızlı kodlama, video ve ayarlanmış **SceneChangeDetection** tootrue, hello Kodlayıcı bir hata döndürür.  
>
>

Şeması hakkında daha fazla bilgi için bkz: [bu](media-services-mes-schema.md) konu.

Tooreview hello emin olun [konuları](#considerations) bölümü.

### <a id="json"></a>JSON hazır
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
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": 640,
              "Height": 360,
            }
          ],
          "Start": "00:00:01",
          "Step": "00:00:10",
          "Range": "00:00:58",
          "Type": "PngImage"
        },
        {
          "BmpLayers": [
            {
              "Type": "BmpLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "10%",
          "Step": "10%",
          "Range": "90%",
          "Type": "BmpImage"
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
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "BmpFormat"
          }
        },
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a id="xml"></a>XML hazır
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
              <Width>640</Width>
              <Height>360</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
        <BmpImage Start="10%" Step="10%" Range="90%">
          <BmpLayers>
            <BmpLayer>
              <Width>640</Width>
              <Height>360</Height>
            </BmpLayer>
          </BmpLayers>
        </BmpImage>
        <PngImage Start="00:00:01" Step="00:00:10" Range="00:00:58">
          <PngLayers>
            <PngLayer>
              <Width>640</Width>
              <Height>360</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <BmpFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

### <a name="considerations"></a>Dikkat edilmesi gerekenler

ilgili önemli noktalar aşağıdaki hello Uygula:

* Merhaba kullanımına açık zaman damgaları Başlat/adım/aralık en az 1 dakika uzun bu hello giriş kaynağı olduğunu varsayar.
* Png/jpg/BmpImage öğeleri başlatma, adım ve dize öznitelikleri aralığı – bu olarak yorumlanacak:

  * Çerçeve sayısı negatif olmayan tamsayılar iseler, örneğin "Başlat": "120",
  * Göreli toosource süresi % sonekine olarak ifade edilen, örneğin "Başlat": "% 15", veya
  * Ss: dd: ifade edilen, zaman damgası... Biçim, örneğin "Başlat": "00: 01:00"

    Karışık ve yazarken gösterimler Lütfen eşleşmesi.

    Ayrıca, başlangıç özel makrosu de destekler: {, hangi toodetermine hello ilk "ilginç" Çerçeve hello içeriğin Not çalışır en iyi}: (adım ve aralığı dikkate alınmaz başlangıç çok ayarlandığında {en iyi})
  * Varsayılan: Başlat: {en iyi}
* Çıktı biçimi açıkça her resim biçimi için sağlanan toobe gerekiyor: Png/Jpg/BmpFormat. Varsa, MES JpgVideo tooJpgFormat vb. eşleşir. Yeni bir görüntü codec belirli makrosu OutputFormat sunar: {, hangi toobe mevcut (bir kez ve yalnızca bir kez) gereken görüntü Çıkış biçimleri için dizin}.

## <a id="trim_video"></a>(Kırpma) video kırpma
Bu bölümde konuşmaları hello Kodlayıcı değiştirme hakkında tooclip hazır ayarları veya hello giriş video hello giriş sözde Ara dosyayı veya isteğe bağlı dosya olduğu kesim. Merhaba Kodlayıcı kullanılan tooclip olması ya da yakalanan veya bir canlı akış alan Arşivlenmiş bir varlık kırpma – bu hello ayrıntılarını kullanılabilir [bu blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).

tootrim videolarınızı belgelenen hello MES hazır hiçbirini uygulayabileceğiniz [bu](media-services-mes-presets-overview.md) bölümünde ve hello değiştirme **kaynakları** (aşağıda gösterildiği gibi) öğesi. StartTime Hello değerini toomatch hello giriş videonun hello mutlak zaman damgaları gerekir. Örneğin, hello hello giriş videonun ilk çerçevesi sahip 12:00:10.000 zaman damgası, sonra StartTime en az olmalıdır 12:00:10.000 büyük. Merhaba aşağıdaki örnekte, hello giriş video başlangıç zaman damgası sıfır olduğunu varsayalım. **Kaynakları** hello hello hazır başında yerleştirilmelidir.

### <a id="json"></a>JSON hazır
    {
      "Version": 1.0,
      "Sources": [
        {
          "StartTime": "00:00:04",
          "Duration": "00:00:16"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 2250,
              "MaxBitrate": 2250,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1500,
              "MaxBitrate": 1500,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1000,
              "MaxBitrate": 1000,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 650,
              "MaxBitrate": 650,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 400,
              "MaxBitrate": 400,
              "BufferWindow": "00:00:05",
              "Width": 320,
              "Height": 180,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="xml-preset"></a>XML hazır
tootrim videolarınızı belgelenen hello MES hazır hiçbirini uygulayabileceğiniz [burada](media-services-mes-presets-overview.md) ve hello değiştirme **kaynakları** (aşağıda gösterildiği gibi) öğesi.

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source StartTime="PT4S" Duration="PT14S"/>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>3400</Bitrate>
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
              <MaxBitrate>3400</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>2250</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>2250</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1500</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1500</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1000</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1000</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>650</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>650</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>400</Bitrate>
              <Width>320</Width>
              <Height>180</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>400</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>

## <a id="overlay"></a>Bir katmana oluşturma

Merhaba Medya Kodlayıcısı standart toooverlay var olan bir video bir görüntüsünü sağlar. Şu anda biçimleri aşağıdaki hello desteklenir: png, jpg, GIF ve bmp. Merhaba aşağıda tanımlanan hazır bir video katmana temel bir örneği bulunmaktadır.

Ayrıca toodefining önceden belirlenmiş bir dosya, ayrıca toolet Media Services bilmeniz hangi hello varlık hello katmana görüntü ve hangi dosya toooverlay hello görüntü istediğiniz hello kaynak video dosyasındadır vardır. Merhaba video dosyası sahip toobe hello **birincil** dosya.

.NET kullanıyorsanız, iki işlevleri toohello .NET örnek tanımlanan aşağıdaki hello ekleyin [bu](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) konu. Merhaba **UploadMediaFilesFromFolder** işlevi (örneğin, BigBuckBunny.mp4 ve Image001.png), bir klasördeki dosyaları karşıya yükleme ve ayarlar hello mp4 dosyası toobe hello birincil dosyasında hello varlık. Merhaba **EncodeWithOverlay** işlevi tooit geçirilen hello özel hazır dosyasını kullanır (örneğin, hello o aşağıdaki önceden) toocreate hello kodlama görev.


    static public IAsset UploadMediaFilesFromFolder(string folderPath)
    {
        IAsset asset = _context.Assets.CreateFromFolder(folderPath, AssetCreationOptions.None);
    
        foreach (var af in asset.AssetFiles)
        {
            // hello following code assumes 
            // you have an input folder with one MP4 and one overlay image file.
            if (af.Name.Contains(".mp4"))
                af.IsPrimary = true;
            else
                af.IsPrimary = false;
    
            af.Update();
        }
    
        return asset;
    }

    static public IAsset EncodeWithOverlay(IAsset assetSource, string customPresetFileName)
    {
        // Declare a new job.
        IJob job = _context.Jobs.Create("Media Encoder Standard Job");
        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(customPresetFileName);

        // Create a task
        ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input assets toobe encoded.
        // This asset contains a source file and an overlay file.
        task.InputAssets.Add(assetSource);

        // Add an output asset toocontain hello results of hello job. 
        task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
        job.Submit();
        job.GetExecutionProgressTask(CancellationToken.None).Wait();

        return job.OutputMediaAssets[0];
    }


> [!NOTE]
> Geçerli sınırlamalar:
>
> Merhaba katmana opaklık ayarı desteklenmiyor.
>
> Kaynak video dosyası ve hello katmana görüntü dosyası aynı varlık hello ve video dosyası gereksinimlerini toobe kümesinin bu varlık hello birincil dosya olarak hello toobe sahip.
>
>

### <a name="json-preset"></a>JSON hazır
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "VideoOverlay": {
              "Position": {
                "X": 100,
                "Y": 100,
                "Width": 100,
                "Height": 50
              },
              "AudioGainLevel": 0.0,
              "MediaParams": [
                {
                  "OverlayLoopCount": 1
                },
                {
                  "IsOverlay": true,
                  "OverlayLoopCount": 1,
                  "InputLoop": true
                }
              ],
              "Source": "Image001.png",
              "Clip": {
                "Duration": "00:00:05"
              },
              "FadeInDuration": {
                "Duration": "00:00:01"
              },
              "FadeOutDuration": {
                "StartTime": "00:00:03",
                "Duration": "00:00:04"
              }
            }
          },
          "Pad": true
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1045,
              "MaxBitrate": 1045,
              "BufferWindow": "00:00:05",
              "ReferenceFrames": 3,
              "EntropyMode": "Cavlc",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Type": "CopyAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}{Extension}",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a name="xml-preset"></a>XML hazır
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source>
          <Streams />
          <Filters>
            <VideoOverlay>
              <Source>Image001.png</Source>
              <Clip Duration="PT5S" />
              <FadeInDuration Duration="PT1S" />
              <FadeOutDuration StartTime="PT3S" Duration="PT4S" />
              <Position X="100" Y="100" Width="100" Height="50" />
              <Opacity>0</Opacity>
              <AudioGainLevel>0</AudioGainLevel>
              <MediaParams>
                <MediaParam>
                  <IsOverlay>false</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>false</InputLoop>
                </MediaParam>
                <MediaParam>
                  <IsOverlay>true</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>true</InputLoop>
                </MediaParam>
              </MediaParams>
            </VideoOverlay>
          </Filters>
          <Pad>true</Pad>
        </Source>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>1045</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>0</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cavlc</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1045</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <CopyAudio />
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}{Extension}">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>


## <a id="silent_audio"></a>Hiç ses giriş sahip olduğunda sessiz bir ses kaydı ekleme
Yalnızca video ve ses yok içeren bir giriş toohello Kodlayıcı gönderirseniz, varsayılan olarak, yalnızca video verileri içeren dosyaları sonra hello çıkış varlık içerir. Bazı oynatıcıları mümkün olmayabilir toohandle böyle çıkış akışları. Bu senaryoda, bu ayar tooforce hello Kodlayıcı tooadd sessiz ses izleme toohello çıkış kullanabilirsiniz.

tooforce hello Kodlayıcı tooproduce hiçbir ses giriş sahip olduğunda, sessiz bir ses parçası içeren bir varlık hello "InsertSilenceIfNoAudio" değerini belirtin.

MES hazır belgelenen hello hiçbirini uygulayabileceğiniz [bu](media-services-mes-presets-overview.md) bölümünde ve hello değişikliği yapın:

### <a name="json-preset"></a>JSON hazır
    {
      "Channels": 2,
      "SamplingRate": 44100,
      "Bitrate": 96,
      "Type": "AACAudio",
      "Condition": "InsertSilenceIfNoAudio"
    }

### <a name="xml-preset"></a>XML hazır
    <AACAudio Condition="InsertSilenceIfNoAudio">
      <Channels>2</Channels>
      <SamplingRate>44100</SamplingRate>
      <Bitrate>96</Bitrate>
    </AACAudio>

## <a id="deinterlacing"></a>XML'deki otomatik taramayı devre dışı bırak
Bunlar hello gibi otomatik olarak XML'deki aralıklı içeriği toobe Taramasız hale getirme, müşterilerin toodo herhangi bir şey gerekmez. Hello XML'deki otomatik taramayı MES hello (varsayılan) hello üzerinde olduğunda otomatik olarak aralıklı çerçeveler algılanmasını ve yalnızca aralıklı olarak işaretlenen çerçeveler XML'deki interlaces.

Hello XML'deki otomatik taramayı kapatabilirsiniz. Bu seçenek önerilmez.

### <a name="json-preset"></a>JSON hazır
    "Sources": [
    {
     "Filters": {
        "Deinterlace": {
          "Mode": "Off"
        }
      },
    }
    ]

### <a name="xml-preset"></a>XML hazır
    <Sources>
    <Source>
      <Filters>
        <Deinterlace>
          <Mode>Off</Mode>
        </Deinterlace>
      </Filters>
    </Source>
    </Sources>


## <a id="audio_only"></a>Yalnızca ses hazır
Bu bölüm iki salt ses MES hazır gösterir: AAC ses ve AAC iyi kaliteli ses.

### <a name="aac-audio"></a>AAC ses
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="aac-good-quality-audio"></a>AAC kaliteli ses
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 192,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <a id="concatenate"></a>İki veya daha fazla video dosyaları birleştirme

Merhaba aşağıdaki örnekte hazır tooconcatenate iki nasıl oluşturacağınız gösterilmiştir veya daha fazla video dosyaları. bir üst bilgi veya toplamı toohello ana video tooadd istediğinizde hello en yaygın senaryodur. Merhaba hello video dosyaları birlikte düzenlenmekte olan özellikleri (ekran çözünürlüğü, kare hızı, ses parça sayısı, vb.) paylaştığınızda kullanım amaçlanmıştır. Toomix videolarınızı değil farklı çerçeve oranlarının ya da ses izleri farklı sayıda ilgilenebilmek.

>[!NOTE]
>Merhaba hello birleştirme özelliğinin geçerli tasarımı bu hello giriş video klip çözümleme bakımından tutarlı bekliyor kare hızı vs. 

### <a name="requirements-and-considerations"></a>Gereksinimleri ve konular

* Giriş videolar yalnızca bir ses parçası olması gerekir.
* Giriş videolar tüm olmalıdır hello aynı kare hızı.
* Videolarınızı ayrı varlıklar karşıya yükleme ve hello videolar her varlık hello birincil dosya olarak ayarlamanız gerekir.
* Videolarınızı tooknow hello süresi gerekir.
* Merhaba hazır örneklere varsayar tüm hello giriş videoları sıfır damgasıyla başlatın. Merhaba videolar farklı başlangıç zaman damgası varsa hello Canlı arşivlerle genelde olduğu gibi toomodify hello StartTime değerleri gerekir.
* Merhaba JSON hazır açık başvurular hello giriş varlıklar toohello AssetID değerlerini sağlar.
* Merhaba örnek kod, JSON önceden bu hello "C:\supportFiles\preset.json" gibi tooa yerel dosya kaydedildi varsayar. Ayrıca, iki varlıklar iki video dosyaları karşıya yükleyerek oluşturulduğunu ve sonuç AssetID değerleri hello biliyorsanız varsayar.
* Merhaba kod parçacığını ve JSON hazır iki video dosyaları birleştirme örneği gösterir. İki videolar tarafından daha toomore genişletebilirsiniz:

  1. Arama görev. InputAssets.Add() art arda tooadd sırayla daha fazla videolar.
  2. Karşılık gelen yapmadan düzenler hello JSON, toohello "Kaynaklar" öğe daha fazla girdi hello ekleyerek aynı sırada.

### <a name="net-code"></a>.NET kodu

    IAsset asset1 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:606db602-efd7-4436-97b4-c0b867ba195b").FirstOrDefault();
    IAsset asset2 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e").FirstOrDefault();

    // Declare a new job.
    IJob job = _context.Jobs.Create("Media Encoder Standard Job for Concatenating Videos");
    // Get a media processor reference, and pass tooit hello name of the
    // processor toouse for hello specific task.
    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

    // Load hello XML (or JSON) from hello local file.
    string configuration = File.ReadAllText(@"c:\supportFiles\preset.json");

    // Create a task
    ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
        processor,
        configuration,
        TaskOptions.None);

    // Specify hello input videos toobe concatenated (in order).
    task.InputAssets.Add(asset1);
    task.InputAssets.Add(asset2);
    // Add an output asset toocontain hello results of hello job.
    // This output is specified as AssetCreationOptions.None, which
    // means hello output asset is not encrypted.
    task.OutputAssets.AddNew("Output asset",
        AssetCreationOptions.None);

    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
    job.Submit();
    job.GetExecutionProgressTask(CancellationToken.None).Wait();

### <a name="json-preset"></a>JSON hazır

Merhaba varlıklar tooconcatenate istediğiniz kimliklerini ve her video hello uygun zaman diliminin önceden özel güncelleştirin.

    {
      "Version": 1.0,
      "Sources": [
        {
          "AssetID": "606db602-efd7-4436-97b4-c0b867ba195b",
          "StartTime": "00:00:01",
          "Duration": "00:00:15"
        },
        {
          "AssetID": "a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e",
          "StartTime": "00:00:02",
          "Duration": "00:00:05"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": true,
          "H264Layers": [
            {
              "Level": "auto",
              "Bitrate": 1800,
              "MaxBitrate": 1800,
              "BufferWindow": "00:00:05",
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
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
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <a id="crop"></a>Medya Kodlayıcısı standart ile kırpma video
Merhaba bkz [kırpma Medya Kodlayıcısı standart ile video](media-services-crop-video.md) konu.

## <a id="no_video"></a>Video giriş sahip olduğunda bir video kaydı ekleme

Yalnızca ses ve video, içeren bir giriş toohello Kodlayıcı gönderirseniz, varsayılan olarak, yalnızca ses verilerini içeren dosyaları sonra hello çıkış varlık içerir. Azure Media Player dahil olmak üzere bazı oynatıcıları (bkz [bu](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) mümkün toohandle böyle akışları olmayabilir. Bu senaryoda tek renkli video izi toohello çıkış, bu ayar tooforce hello Kodlayıcı tooadd kullanabilirsiniz.

> [!NOTE]
> Merhaba Kodlayıcı tooinsert zorlama bir çıktı video izleme artar hello boyutunu hello varlık çıkış ve böylece görev kodlama Merhaba ücrete maliyet hello. Bu testleri tooverify çalışması gerektiğini sonuç bu artış, Aylık Ücretler üzerinde yalnızca uygun bir etkisi yoktur.
>

### <a name="inserting-video-at-only-hello-lowest-bitrate"></a>Yalnızca hello düşük bit hızlı video ekleme

Bir Çoklu bit hızı gibi önceden kodlama kullanıyorsanız varsayalım ["H264 Çoklu bit hızı 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) tüm giriş video dosyaları ve yalnızca ses dosyaları bir karışımını içeren akış, katalog tooencode. Bu senaryoda, hiçbir video Hello giriş sahip olduğunda tooforce hello Kodlayıcı tooinsert tek renkli video karşılıklı tooinserting her çıktı bit hızı video olarak yalnızca hello düşük bit hızlı, izlemek isteyebilir. tooachieve bunu toouse hello gereksinim **InsertBlackIfNoVideoBottomLayerOnly** bayrağı.

MES hazır belgelenen hello hiçbirini uygulayabileceğiniz [bu](media-services-mes-presets-overview.md) bölümünde ve hello değişikliği yapın:

#### <a name="json-preset"></a>JSON hazır
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideoBottomLayerOnly",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a>XML hazır

XML, koşul kullanırken bir öznitelik toohello olarak "InsertBlackIfNoVideoBottomLayerOnly" = **H264Video** öğesi ve koşul "InsertSilenceIfNoAudio" öznitelik olarak çok =**AACAudio**.

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideoBottomLayerOnly">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .
```

### <a name="inserting-video-at-all-output-bitrates"></a>Bit çıkış video hiç ekleme
Bir Çoklu bit hızı gibi önceden kodlama kullanıyorsanız varsayalım ["H264 Çoklu bit hızı 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) bütün giriş video dosyaları ve yalnızca ses dosyaları bir karışımını içeren akış, katalog tooencode. Bu senaryoda, hiçbir video Hello giriş sahip olduğunda, tek renkli bir video izlemek tüm hello çıkış bit tooforce hello Kodlayıcı tooinsert isteyebilirsiniz. Bu, çıktı sağlar varlıklar ile video izler ve ses izleri saygı toonumber tüm homojen. tooachieve bunu toospecify hello "InsertBlackIfNoVideo" bayrağı gerekir.

MES hazır belgelenen hello hiçbirini uygulayabileceğiniz [bu](media-services-mes-presets-overview.md) bölümünde ve hello değişikliği yapın:

#### <a name="json-preset"></a>JSON hazır
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideo",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a>XML hazır

XML, koşul kullanırken bir öznitelik toohello olarak "InsertBlackIfNoVideo" = **H264Video** öğesi ve koşul "InsertSilenceIfNoAudio" öznitelik olarak çok =**AACAudio**.

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideo">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .  
```

## <a id="rotate_video"></a>Bir video Döndür
Merhaba [Medya Kodlayıcısı standart](media-services-dotnet-encode-with-media-encoder-standard.md) 0/90/180/270 açıları tarafından dönüşünü destekler. "Auto", burada toodetect hello döndürme meta verilerde hello gelen video dosyası çalışır ve için dengelemek Hello varsayılan davranıştır. Merhaba şunlar **kaynakları** öğesi tooone tanımlanan hello hazır [bu](media-services-mes-presets-overview.md) bölümü:

### <a name="json-preset"></a>JSON hazır
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...
### <a name="xml-preset"></a>XML hazır
    <Sources>
           <Source>
          <Streams />
          <Filters>
            <Rotation>90</Rotation>
          </Filters>
        </Source>
    </Sources>

Ayrıca bkz [bu](media-services-mes-schema.md#PreserveResolutionAfterRotation) döndürme maaş tetiklendiğinde konu hello Kodlayıcı hello genişlik ve yükseklik ayarlarında hello yorumlaması hakkında daha fazla bilgi için hazır.

Merhaba "0" değerini tooindicate toohello Kodlayıcı tooignore döndürme meta verileri, varsa hello giriş videoda kullanabilirsiniz.

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Ayrıca Bkz.
[Media Services kodlama a genel bakış](media-services-encode-asset.md)
