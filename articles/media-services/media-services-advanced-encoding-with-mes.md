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
# <a name="perform-advanced-encoding-by-customizing-mes-presets"></a><span data-ttu-id="b0046-103">Gelişmiş kodlama MES hazır ayarlarını özelleştirerek gerçekleştirin</span><span class="sxs-lookup"><span data-stu-id="b0046-103">Perform advanced encoding by customizing MES presets</span></span> 

## <a name="overview"></a><span data-ttu-id="b0046-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b0046-104">Overview</span></span>

<span data-ttu-id="b0046-105">Bu konuda nasıl toocustomize Medya Kodlayıcısı standart hazır ayarları gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b0046-105">This topic shows how toocustomize Media Encoder Standard presets.</span></span> <span data-ttu-id="b0046-106">Merhaba [Medya Kodlayıcısı özel hazır ayarları kullanarak standart ile kodlama](media-services-custom-mes-presets-with-dotnet.md) konu, nasıl bir kodlama toouse .NET toocreate görev ve bu görevi yürüten bir işi gösterir.</span><span class="sxs-lookup"><span data-stu-id="b0046-106">hello [Encoding with Media Encoder Standard using custom presets](media-services-custom-mes-presets-with-dotnet.md) topic shows how toouse .NET toocreate an encoding task and a job that executes this task.</span></span> <span data-ttu-id="b0046-107">Bir hazır tedarik hello özel hazır toohello kodlama görev özelleştirildikten sonra.</span><span class="sxs-lookup"><span data-stu-id="b0046-107">Once you customize a preset, supply hello custom presets toohello encoding task.</span></span> 

>[!NOTE]
><span data-ttu-id="b0046-108">Bir XML hazır kullanıyorsanız, XML örneklerinde aşağıda gösterildiği gibi öğeleri emin toopreserve hello sırasını olun (örneğin, KeyFrameInterval SceneChangeDetection gelmelidir).</span><span class="sxs-lookup"><span data-stu-id="b0046-108">If using an XML preset, make sure toopreserve hello order of elements, as shown in XML samples below (for example, KeyFrameInterval should precede SceneChangeDetection).</span></span>
>

<span data-ttu-id="b0046-109">Bu konuda, kodlama görevleri aşağıdaki hello gerçekleştirmek hello özel hazır gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b0046-109">In this topic, hello custom presets that perform hello following encoding tasks are demonstrated.</span></span>

## <a name="support-for-relative-sizes"></a><span data-ttu-id="b0046-110">Göreli boyutları için destek</span><span class="sxs-lookup"><span data-stu-id="b0046-110">Support for relative sizes</span></span>

<span data-ttu-id="b0046-111">Küçük resimleri oluştururken, gereksinim tooalways çıkış genişlik ve yükseklik piksel cinsinden belirtin.</span><span class="sxs-lookup"><span data-stu-id="b0046-111">When generating thumbnails, you do not need tooalways specify output width and height in pixels.</span></span> <span data-ttu-id="b0046-112">[% 1,..., % 100] hello aralıktaki yüzde belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0046-112">You can specify them in percentages, in hello range [1%, …, 100%].</span></span>

### <a name="json-preset"></a><span data-ttu-id="b0046-113">JSON hazır</span><span class="sxs-lookup"><span data-stu-id="b0046-113">JSON preset</span></span>
    "Width": "100%",
    "Height": "100%"

### <a name="xml-preset"></a><span data-ttu-id="b0046-114">XML hazır</span><span class="sxs-lookup"><span data-stu-id="b0046-114">XML preset</span></span>
    <Width>100%</Width>
    <Height>100%</Height>

## <span data-ttu-id="b0046-115"><a id="thumbnails"></a>Küçük resimler oluşturma</span><span class="sxs-lookup"><span data-stu-id="b0046-115"><a id="thumbnails"></a>Generate thumbnails</span></span>

<span data-ttu-id="b0046-116">Bu bölümde gösterilmiştir nasıl toocustomize küçük resim oluşturur hazır.</span><span class="sxs-lookup"><span data-stu-id="b0046-116">This section shows how toocustomize a preset that generates thumbnails.</span></span> <span data-ttu-id="b0046-117">Merhaba aşağıda tanımlanan hazır tooencode istediğiniz bilgi dosyanızı yanı sıra toogenerate küçük resimleri gerekli bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="b0046-117">hello preset defined below contains information on how you want tooencode your file as well as information needed toogenerate thumbnails.</span></span> <span data-ttu-id="b0046-118">Merhaba MES hazır belgelenen hiçbirini uygulayabileceğiniz [bu](media-services-mes-presets-overview.md) bölümünde ve küçük resim oluşturur kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b0046-118">You can take any of hello MES presets documented [this](media-services-mes-presets-overview.md) section and add code that generates thumbnails.</span></span>  

> [!NOTE]
> <span data-ttu-id="b0046-119">Merhaba **SceneChangeDetection** hazır aşağıdaki hello ayarında yalnızca ayarlanabilir tootrue tooa tek bit hızlı video kodlama durumunda.</span><span class="sxs-lookup"><span data-stu-id="b0046-119">hello **SceneChangeDetection** setting in hello following preset can only be set tootrue if you are encoding tooa single  bitrate video.</span></span> <span data-ttu-id="b0046-120">Tooa Çoklu bit hızlı kodlama, video ve ayarlanmış **SceneChangeDetection** tootrue, hello Kodlayıcı bir hata döndürür.</span><span class="sxs-lookup"><span data-stu-id="b0046-120">If you are encoding tooa multi-bitrate video and set **SceneChangeDetection** tootrue, hello encoder returns an error.</span></span>  
>
>

<span data-ttu-id="b0046-121">Şeması hakkında daha fazla bilgi için bkz: [bu](media-services-mes-schema.md) konu.</span><span class="sxs-lookup"><span data-stu-id="b0046-121">For information about schema, see [this](media-services-mes-schema.md) topic.</span></span>

<span data-ttu-id="b0046-122">Tooreview hello emin olun [konuları](#considerations) bölümü.</span><span class="sxs-lookup"><span data-stu-id="b0046-122">Make sure tooreview hello [Considerations](#considerations) section.</span></span>

### <span data-ttu-id="b0046-123"><a id="json"></a>JSON hazır</span><span class="sxs-lookup"><span data-stu-id="b0046-123"><a id="json"></a>JSON preset</span></span>
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


### <span data-ttu-id="b0046-124"><a id="xml"></a>XML hazır</span><span class="sxs-lookup"><span data-stu-id="b0046-124"><a id="xml"></a>XML preset</span></span>
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

### <a name="considerations"></a><span data-ttu-id="b0046-125">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="b0046-125">Considerations</span></span>

<span data-ttu-id="b0046-126">ilgili önemli noktalar aşağıdaki hello Uygula:</span><span class="sxs-lookup"><span data-stu-id="b0046-126">hello following considerations apply:</span></span>

* <span data-ttu-id="b0046-127">Merhaba kullanımına açık zaman damgaları Başlat/adım/aralık en az 1 dakika uzun bu hello giriş kaynağı olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="b0046-127">hello use of explicit timestamps for Start/Step/Range assumes that hello input source is at least 1 minute long.</span></span>
* <span data-ttu-id="b0046-128">Png/jpg/BmpImage öğeleri başlatma, adım ve dize öznitelikleri aralığı – bu olarak yorumlanacak:</span><span class="sxs-lookup"><span data-stu-id="b0046-128">Jpg/Png/BmpImage elements have Start, Step, and Range string attributes – these can be interpreted as:</span></span>

  * <span data-ttu-id="b0046-129">Çerçeve sayısı negatif olmayan tamsayılar iseler, örneğin "Başlat": "120",</span><span class="sxs-lookup"><span data-stu-id="b0046-129">Frame Number if they are non-negative integers, for example "Start": "120",</span></span>
  * <span data-ttu-id="b0046-130">Göreli toosource süresi % sonekine olarak ifade edilen, örneğin "Başlat": "% 15", veya</span><span class="sxs-lookup"><span data-stu-id="b0046-130">Relative toosource duration if expressed as %-suffixed, for example "Start": "15%", OR</span></span>
  * <span data-ttu-id="b0046-131">Ss: dd: ifade edilen, zaman damgası...</span><span class="sxs-lookup"><span data-stu-id="b0046-131">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="b0046-132">Biçim, örneğin "Başlat": "00: 01:00"</span><span class="sxs-lookup"><span data-stu-id="b0046-132">format, for example "Start" : "00:01:00"</span></span>

    <span data-ttu-id="b0046-133">Karışık ve yazarken gösterimler Lütfen eşleşmesi.</span><span class="sxs-lookup"><span data-stu-id="b0046-133">You can mix and match notations as you please.</span></span>

    <span data-ttu-id="b0046-134">Ayrıca, başlangıç özel makrosu de destekler: {, hangi toodetermine hello ilk "ilginç" Çerçeve hello içeriğin Not çalışır en iyi}: (adım ve aralığı dikkate alınmaz başlangıç çok ayarlandığında {en iyi})</span><span class="sxs-lookup"><span data-stu-id="b0046-134">Additionally, Start also supports a special Macro:{Best}, which attempts toodetermine hello first “interesting” frame of hello content NOTE: (Step and Range are ignored when Start is set too{Best})</span></span>
  * <span data-ttu-id="b0046-135">Varsayılan: Başlat: {en iyi}</span><span class="sxs-lookup"><span data-stu-id="b0046-135">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="b0046-136">Çıktı biçimi açıkça her resim biçimi için sağlanan toobe gerekiyor: Png/Jpg/BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="b0046-136">Output format needs toobe explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="b0046-137">Varsa, MES JpgVideo tooJpgFormat vb. eşleşir.</span><span class="sxs-lookup"><span data-stu-id="b0046-137">When present, MES matches JpgVideo tooJpgFormat and so on.</span></span> <span data-ttu-id="b0046-138">Yeni bir görüntü codec belirli makrosu OutputFormat sunar: {, hangi toobe mevcut (bir kez ve yalnızca bir kez) gereken görüntü Çıkış biçimleri için dizin}.</span><span class="sxs-lookup"><span data-stu-id="b0046-138">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs toobe present (once and only once) for image output formats.</span></span>

## <span data-ttu-id="b0046-139"><a id="trim_video"></a>(Kırpma) video kırpma</span><span class="sxs-lookup"><span data-stu-id="b0046-139"><a id="trim_video"></a>Trim a video (clipping)</span></span>
<span data-ttu-id="b0046-140">Bu bölümde konuşmaları hello Kodlayıcı değiştirme hakkında tooclip hazır ayarları veya hello giriş video hello giriş sözde Ara dosyayı veya isteğe bağlı dosya olduğu kesim.</span><span class="sxs-lookup"><span data-stu-id="b0046-140">This section talks about modifying hello encoder presets tooclip or trim hello input video where hello input is a so-called mezzanine file or on-demand file.</span></span> <span data-ttu-id="b0046-141">Merhaba Kodlayıcı kullanılan tooclip olması ya da yakalanan veya bir canlı akış alan Arşivlenmiş bir varlık kırpma – bu hello ayrıntılarını kullanılabilir [bu blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="b0046-141">hello encoder can also be used tooclip or trim an asset, which is captured or archived from a live stream – hello details for this are available in [this blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span></span>

<span data-ttu-id="b0046-142">tootrim videolarınızı belgelenen hello MES hazır hiçbirini uygulayabileceğiniz [bu](media-services-mes-presets-overview.md) bölümünde ve hello değiştirme **kaynakları** (aşağıda gösterildiği gibi) öğesi.</span><span class="sxs-lookup"><span data-stu-id="b0046-142">tootrim your videos, you can take any of hello MES presets documented [this](media-services-mes-presets-overview.md) section and modify hello **Sources** element (as shown below).</span></span> <span data-ttu-id="b0046-143">StartTime Hello değerini toomatch hello giriş videonun hello mutlak zaman damgaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0046-143">hello value of StartTime needs toomatch hello absolute timestamps of hello input video.</span></span> <span data-ttu-id="b0046-144">Örneğin, hello hello giriş videonun ilk çerçevesi sahip 12:00:10.000 zaman damgası, sonra StartTime en az olmalıdır 12:00:10.000 büyük.</span><span class="sxs-lookup"><span data-stu-id="b0046-144">For example, if hello first frame of hello input video has a timestamp of 12:00:10.000, then StartTime should be at least 12:00:10.000 and greater.</span></span> <span data-ttu-id="b0046-145">Merhaba aşağıdaki örnekte, hello giriş video başlangıç zaman damgası sıfır olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="b0046-145">In hello example below, we assume that hello input video has a starting timestamp of zero.</span></span> <span data-ttu-id="b0046-146">**Kaynakları** hello hello hazır başında yerleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="b0046-146">**Sources** should be placed at hello beginning of hello preset.</span></span>

### <span data-ttu-id="b0046-147"><a id="json"></a>JSON hazır</span><span class="sxs-lookup"><span data-stu-id="b0046-147"><a id="json"></a>JSON preset</span></span>
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

### <a name="xml-preset"></a><span data-ttu-id="b0046-148">XML hazır</span><span class="sxs-lookup"><span data-stu-id="b0046-148">XML preset</span></span>
<span data-ttu-id="b0046-149">tootrim videolarınızı belgelenen hello MES hazır hiçbirini uygulayabileceğiniz [burada](media-services-mes-presets-overview.md) ve hello değiştirme **kaynakları** (aşağıda gösterildiği gibi) öğesi.</span><span class="sxs-lookup"><span data-stu-id="b0046-149">tootrim your videos, you can take any of hello MES presets documented [here](media-services-mes-presets-overview.md) and modify hello **Sources** element (as shown below).</span></span>

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

## <span data-ttu-id="b0046-150"><a id="overlay"></a>Bir katmana oluşturma</span><span class="sxs-lookup"><span data-stu-id="b0046-150"><a id="overlay"></a>Create an overlay</span></span>

<span data-ttu-id="b0046-151">Merhaba Medya Kodlayıcısı standart toooverlay var olan bir video bir görüntüsünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="b0046-151">hello Media Encoder Standard allows you toooverlay an image onto an existing video.</span></span> <span data-ttu-id="b0046-152">Şu anda biçimleri aşağıdaki hello desteklenir: png, jpg, GIF ve bmp.</span><span class="sxs-lookup"><span data-stu-id="b0046-152">Currently, hello following formats are supported: png, jpg, gif, and bmp.</span></span> <span data-ttu-id="b0046-153">Merhaba aşağıda tanımlanan hazır bir video katmana temel bir örneği bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b0046-153">hello preset defined below is a basic example  of a video overlay.</span></span>

<span data-ttu-id="b0046-154">Ayrıca toodefining önceden belirlenmiş bir dosya, ayrıca toolet Media Services bilmeniz hangi hello varlık hello katmana görüntü ve hangi dosya toooverlay hello görüntü istediğiniz hello kaynak video dosyasındadır vardır.</span><span class="sxs-lookup"><span data-stu-id="b0046-154">In addition toodefining a preset file, you also have toolet Media Services know which file in hello asset is hello overlay image and which file is hello source video onto which you want toooverlay hello image.</span></span> <span data-ttu-id="b0046-155">Merhaba video dosyası sahip toobe hello **birincil** dosya.</span><span class="sxs-lookup"><span data-stu-id="b0046-155">hello video file has toobe hello **primary** file.</span></span>

<span data-ttu-id="b0046-156">.NET kullanıyorsanız, iki işlevleri toohello .NET örnek tanımlanan aşağıdaki hello ekleyin [bu](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) konu.</span><span class="sxs-lookup"><span data-stu-id="b0046-156">If you are using .NET, add hello following two functions toohello .NET example defined in [this](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic.</span></span> <span data-ttu-id="b0046-157">Merhaba **UploadMediaFilesFromFolder** işlevi (örneğin, BigBuckBunny.mp4 ve Image001.png), bir klasördeki dosyaları karşıya yükleme ve ayarlar hello mp4 dosyası toobe hello birincil dosyasında hello varlık.</span><span class="sxs-lookup"><span data-stu-id="b0046-157">hello **UploadMediaFilesFromFolder** function uploads files from a folder (for example, BigBuckBunny.mp4 and Image001.png) and sets hello mp4 file toobe hello primary file in hello asset.</span></span> <span data-ttu-id="b0046-158">Merhaba **EncodeWithOverlay** işlevi tooit geçirilen hello özel hazır dosyasını kullanır (örneğin, hello o aşağıdaki önceden) toocreate hello kodlama görev.</span><span class="sxs-lookup"><span data-stu-id="b0046-158">hello **EncodeWithOverlay** function uses hello custom preset file that was passed tooit (for example, hello preset that follows) toocreate hello encoding task.</span></span>


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
> <span data-ttu-id="b0046-159">Geçerli sınırlamalar:</span><span class="sxs-lookup"><span data-stu-id="b0046-159">Current limitations:</span></span>
>
> <span data-ttu-id="b0046-160">Merhaba katmana opaklık ayarı desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="b0046-160">hello overlay opacity setting is not supported.</span></span>
>
> <span data-ttu-id="b0046-161">Kaynak video dosyası ve hello katmana görüntü dosyası aynı varlık hello ve video dosyası gereksinimlerini toobe kümesinin bu varlık hello birincil dosya olarak hello toobe sahip.</span><span class="sxs-lookup"><span data-stu-id="b0046-161">Your source video file and hello overlay image file have toobe in hello same asset, and hello video file needs toobe set as hello primary file in this asset.</span></span>
>
>

### <a name="json-preset"></a><span data-ttu-id="b0046-162">JSON hazır</span><span class="sxs-lookup"><span data-stu-id="b0046-162">JSON preset</span></span>
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


### <a name="xml-preset"></a><span data-ttu-id="b0046-163">XML hazır</span><span class="sxs-lookup"><span data-stu-id="b0046-163">XML preset</span></span>
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


## <span data-ttu-id="b0046-164"><a id="silent_audio"></a>Hiç ses giriş sahip olduğunda sessiz bir ses kaydı ekleme</span><span class="sxs-lookup"><span data-stu-id="b0046-164"><a id="silent_audio"></a>Insert a silent audio track when input has no audio</span></span>
<span data-ttu-id="b0046-165">Yalnızca video ve ses yok içeren bir giriş toohello Kodlayıcı gönderirseniz, varsayılan olarak, yalnızca video verileri içeren dosyaları sonra hello çıkış varlık içerir.</span><span class="sxs-lookup"><span data-stu-id="b0046-165">By default, if you send an input toohello encoder that contains only video, and no audio, then hello output asset contains files that contain only video data.</span></span> <span data-ttu-id="b0046-166">Bazı oynatıcıları mümkün olmayabilir toohandle böyle çıkış akışları.</span><span class="sxs-lookup"><span data-stu-id="b0046-166">Some players may not be able toohandle such output streams.</span></span> <span data-ttu-id="b0046-167">Bu senaryoda, bu ayar tooforce hello Kodlayıcı tooadd sessiz ses izleme toohello çıkış kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0046-167">You can use this setting tooforce hello encoder tooadd a silent audio track toohello output in that scenario.</span></span>

<span data-ttu-id="b0046-168">tooforce hello Kodlayıcı tooproduce hiçbir ses giriş sahip olduğunda, sessiz bir ses parçası içeren bir varlık hello "InsertSilenceIfNoAudio" değerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="b0046-168">tooforce hello encoder tooproduce an asset that contains a silent audio track when input has no audio, specify hello "InsertSilenceIfNoAudio" value.</span></span>

<span data-ttu-id="b0046-169">MES hazır belgelenen hello hiçbirini uygulayabileceğiniz [bu](media-services-mes-presets-overview.md) bölümünde ve hello değişikliği yapın:</span><span class="sxs-lookup"><span data-stu-id="b0046-169">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

### <a name="json-preset"></a><span data-ttu-id="b0046-170">JSON hazır</span><span class="sxs-lookup"><span data-stu-id="b0046-170">JSON preset</span></span>
    {
      "Channels": 2,
      "SamplingRate": 44100,
      "Bitrate": 96,
      "Type": "AACAudio",
      "Condition": "InsertSilenceIfNoAudio"
    }

### <a name="xml-preset"></a><span data-ttu-id="b0046-171">XML hazır</span><span class="sxs-lookup"><span data-stu-id="b0046-171">XML preset</span></span>
    <AACAudio Condition="InsertSilenceIfNoAudio">
      <Channels>2</Channels>
      <SamplingRate>44100</SamplingRate>
      <Bitrate>96</Bitrate>
    </AACAudio>

## <span data-ttu-id="b0046-172"><a id="deinterlacing"></a>XML'deki otomatik taramayı devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="b0046-172"><a id="deinterlacing"></a>Disable auto de-interlacing</span></span>
<span data-ttu-id="b0046-173">Bunlar hello gibi otomatik olarak XML'deki aralıklı içeriği toobe Taramasız hale getirme, müşterilerin toodo herhangi bir şey gerekmez.</span><span class="sxs-lookup"><span data-stu-id="b0046-173">Customers don’t need toodo anything if they like hello interlace contents toobe automatically de-interlaced.</span></span> <span data-ttu-id="b0046-174">Hello XML'deki otomatik taramayı MES hello (varsayılan) hello üzerinde olduğunda otomatik olarak aralıklı çerçeveler algılanmasını ve yalnızca aralıklı olarak işaretlenen çerçeveler XML'deki interlaces.</span><span class="sxs-lookup"><span data-stu-id="b0046-174">When hello auto de-interlacing is on (default) hello MES does hello auto detection of interlaced frames and only de-interlaces frames marked as interlaced.</span></span>

<span data-ttu-id="b0046-175">Hello XML'deki otomatik taramayı kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0046-175">You can turn hello auto de-interlacing off.</span></span> <span data-ttu-id="b0046-176">Bu seçenek önerilmez.</span><span class="sxs-lookup"><span data-stu-id="b0046-176">This option is not recommended.</span></span>

### <a name="json-preset"></a><span data-ttu-id="b0046-177">JSON hazır</span><span class="sxs-lookup"><span data-stu-id="b0046-177">JSON preset</span></span>
    "Sources": [
    {
     "Filters": {
        "Deinterlace": {
          "Mode": "Off"
        }
      },
    }
    ]

### <a name="xml-preset"></a><span data-ttu-id="b0046-178">XML hazır</span><span class="sxs-lookup"><span data-stu-id="b0046-178">XML preset</span></span>
    <Sources>
    <Source>
      <Filters>
        <Deinterlace>
          <Mode>Off</Mode>
        </Deinterlace>
      </Filters>
    </Source>
    </Sources>


## <span data-ttu-id="b0046-179"><a id="audio_only"></a>Yalnızca ses hazır</span><span class="sxs-lookup"><span data-stu-id="b0046-179"><a id="audio_only"></a>Audio-only presets</span></span>
<span data-ttu-id="b0046-180">Bu bölüm iki salt ses MES hazır gösterir: AAC ses ve AAC iyi kaliteli ses.</span><span class="sxs-lookup"><span data-stu-id="b0046-180">This section demonstrates two audio-only MES presets: AAC Audio and AAC Good Quality Audio.</span></span>

### <a name="aac-audio"></a><span data-ttu-id="b0046-181">AAC ses</span><span class="sxs-lookup"><span data-stu-id="b0046-181">AAC Audio</span></span>
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

### <a name="aac-good-quality-audio"></a><span data-ttu-id="b0046-182">AAC kaliteli ses</span><span class="sxs-lookup"><span data-stu-id="b0046-182">AAC Good Quality Audio</span></span>
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

## <span data-ttu-id="b0046-183"><a id="concatenate"></a>İki veya daha fazla video dosyaları birleştirme</span><span class="sxs-lookup"><span data-stu-id="b0046-183"><a id="concatenate"></a>Concatenate two or more video files</span></span>

<span data-ttu-id="b0046-184">Merhaba aşağıdaki örnekte hazır tooconcatenate iki nasıl oluşturacağınız gösterilmiştir veya daha fazla video dosyaları.</span><span class="sxs-lookup"><span data-stu-id="b0046-184">hello following example illustrates how you can generate a preset tooconcatenate two or more video files.</span></span> <span data-ttu-id="b0046-185">bir üst bilgi veya toplamı toohello ana video tooadd istediğinizde hello en yaygın senaryodur.</span><span class="sxs-lookup"><span data-stu-id="b0046-185">hello most common scenario is when you want tooadd a header or a trailer toohello main video.</span></span> <span data-ttu-id="b0046-186">Merhaba hello video dosyaları birlikte düzenlenmekte olan özellikleri (ekran çözünürlüğü, kare hızı, ses parça sayısı, vb.) paylaştığınızda kullanım amaçlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b0046-186">hello intended use is when hello video files being edited together share  properties (video resolution, frame rate, audio track count, etc.).</span></span> <span data-ttu-id="b0046-187">Toomix videolarınızı değil farklı çerçeve oranlarının ya da ses izleri farklı sayıda ilgilenebilmek.</span><span class="sxs-lookup"><span data-stu-id="b0046-187">You should take care not toomix videos of different frame rates, or with different number of audio tracks.</span></span>

>[!NOTE]
><span data-ttu-id="b0046-188">Merhaba hello birleştirme özelliğinin geçerli tasarımı bu hello giriş video klip çözümleme bakımından tutarlı bekliyor kare hızı vs.</span><span class="sxs-lookup"><span data-stu-id="b0046-188">hello current design of hello concatenation feature expects that hello input video clips are consistent in terms of resolution, frame rate etc.</span></span> 

### <a name="requirements-and-considerations"></a><span data-ttu-id="b0046-189">Gereksinimleri ve konular</span><span class="sxs-lookup"><span data-stu-id="b0046-189">Requirements and considerations</span></span>

* <span data-ttu-id="b0046-190">Giriş videolar yalnızca bir ses parçası olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0046-190">Input videos should only have one audio track.</span></span>
* <span data-ttu-id="b0046-191">Giriş videolar tüm olmalıdır hello aynı kare hızı.</span><span class="sxs-lookup"><span data-stu-id="b0046-191">Input videos should all have hello same frame rate.</span></span>
* <span data-ttu-id="b0046-192">Videolarınızı ayrı varlıklar karşıya yükleme ve hello videolar her varlık hello birincil dosya olarak ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0046-192">You must upload your videos into separate assets and set hello videos as hello primary file in each asset.</span></span>
* <span data-ttu-id="b0046-193">Videolarınızı tooknow hello süresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0046-193">You need tooknow hello duration of your videos.</span></span>
* <span data-ttu-id="b0046-194">Merhaba hazır örneklere varsayar tüm hello giriş videoları sıfır damgasıyla başlatın.</span><span class="sxs-lookup"><span data-stu-id="b0046-194">hello preset examples below assumes that all hello input videos start with a timestamp of zero.</span></span> <span data-ttu-id="b0046-195">Merhaba videolar farklı başlangıç zaman damgası varsa hello Canlı arşivlerle genelde olduğu gibi toomodify hello StartTime değerleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0046-195">You need toomodify hello StartTime values if hello videos have different starting timestamp, as is typically hello case with live archives.</span></span>
* <span data-ttu-id="b0046-196">Merhaba JSON hazır açık başvurular hello giriş varlıklar toohello AssetID değerlerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="b0046-196">hello JSON preset makes explicit references toohello AssetID values of hello input assets.</span></span>
* <span data-ttu-id="b0046-197">Merhaba örnek kod, JSON önceden bu hello "C:\supportFiles\preset.json" gibi tooa yerel dosya kaydedildi varsayar.</span><span class="sxs-lookup"><span data-stu-id="b0046-197">hello sample code assumes that hello JSON preset has been saved tooa local file, such as "C:\supportFiles\preset.json".</span></span> <span data-ttu-id="b0046-198">Ayrıca, iki varlıklar iki video dosyaları karşıya yükleyerek oluşturulduğunu ve sonuç AssetID değerleri hello biliyorsanız varsayar.</span><span class="sxs-lookup"><span data-stu-id="b0046-198">It also assumes that two assets have been created by uploading two video files, and that you know hello resultant AssetID values.</span></span>
* <span data-ttu-id="b0046-199">Merhaba kod parçacığını ve JSON hazır iki video dosyaları birleştirme örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="b0046-199">hello code snippet and JSON preset shows an example of concatenating two video files.</span></span> <span data-ttu-id="b0046-200">İki videolar tarafından daha toomore genişletebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b0046-200">You can extend it toomore than two videos by:</span></span>

  1. <span data-ttu-id="b0046-201">Arama görev. InputAssets.Add() art arda tooadd sırayla daha fazla videolar.</span><span class="sxs-lookup"><span data-stu-id="b0046-201">Calling task.InputAssets.Add() repeatedly tooadd more videos, in order.</span></span>
  2. <span data-ttu-id="b0046-202">Karşılık gelen yapmadan düzenler hello JSON, toohello "Kaynaklar" öğe daha fazla girdi hello ekleyerek aynı sırada.</span><span class="sxs-lookup"><span data-stu-id="b0046-202">Making corresponding edits toohello "Sources" element in hello JSON, by adding more entries, in hello same order.</span></span>

### <a name="net-code"></a><span data-ttu-id="b0046-203">.NET kodu</span><span class="sxs-lookup"><span data-stu-id="b0046-203">.NET code</span></span>

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

### <a name="json-preset"></a><span data-ttu-id="b0046-204">JSON hazır</span><span class="sxs-lookup"><span data-stu-id="b0046-204">JSON preset</span></span>

<span data-ttu-id="b0046-205">Merhaba varlıklar tooconcatenate istediğiniz kimliklerini ve her video hello uygun zaman diliminin önceden özel güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="b0046-205">Update your custom preset with ids of hello assets that you want tooconcatenate, and with hello appropriate time segment for each video.</span></span>

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

## <span data-ttu-id="b0046-206"><a id="crop"></a>Medya Kodlayıcısı standart ile kırpma video</span><span class="sxs-lookup"><span data-stu-id="b0046-206"><a id="crop"></a>Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="b0046-207">Merhaba bkz [kırpma Medya Kodlayıcısı standart ile video](media-services-crop-video.md) konu.</span><span class="sxs-lookup"><span data-stu-id="b0046-207">See hello [Crop videos with Media Encoder Standard](media-services-crop-video.md) topic.</span></span>

## <span data-ttu-id="b0046-208"><a id="no_video"></a>Video giriş sahip olduğunda bir video kaydı ekleme</span><span class="sxs-lookup"><span data-stu-id="b0046-208"><a id="no_video"></a>Insert a video track when input has no video</span></span>

<span data-ttu-id="b0046-209">Yalnızca ses ve video, içeren bir giriş toohello Kodlayıcı gönderirseniz, varsayılan olarak, yalnızca ses verilerini içeren dosyaları sonra hello çıkış varlık içerir.</span><span class="sxs-lookup"><span data-stu-id="b0046-209">By default, if you send an input toohello encoder that contains only audio, and no video, then hello output asset contains files that contain only audio data.</span></span> <span data-ttu-id="b0046-210">Azure Media Player dahil olmak üzere bazı oynatıcıları (bkz [bu](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) mümkün toohandle böyle akışları olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="b0046-210">Some players, including Azure Media Player (see [this](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) may not be able toohandle such streams.</span></span> <span data-ttu-id="b0046-211">Bu senaryoda tek renkli video izi toohello çıkış, bu ayar tooforce hello Kodlayıcı tooadd kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0046-211">You can use this setting tooforce hello encoder tooadd a monochrome video track toohello output in that scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="b0046-212">Merhaba Kodlayıcı tooinsert zorlama bir çıktı video izleme artar hello boyutunu hello varlık çıkış ve böylece görev kodlama Merhaba ücrete maliyet hello.</span><span class="sxs-lookup"><span data-stu-id="b0046-212">Forcing hello encoder tooinsert an output video track increases hello size of hello output Asset, and thereby hello cost incurred for hello encoding Task.</span></span> <span data-ttu-id="b0046-213">Bu testleri tooverify çalışması gerektiğini sonuç bu artış, Aylık Ücretler üzerinde yalnızca uygun bir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="b0046-213">You should run tests tooverify that this resultant increase has only a modest impact on your monthly charges.</span></span>
>

### <a name="inserting-video-at-only-hello-lowest-bitrate"></a><span data-ttu-id="b0046-214">Yalnızca hello düşük bit hızlı video ekleme</span><span class="sxs-lookup"><span data-stu-id="b0046-214">Inserting video at only hello lowest bitrate</span></span>

<span data-ttu-id="b0046-215">Bir Çoklu bit hızı gibi önceden kodlama kullanıyorsanız varsayalım ["H264 Çoklu bit hızı 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) tüm giriş video dosyaları ve yalnızca ses dosyaları bir karışımını içeren akış, katalog tooencode.</span><span class="sxs-lookup"><span data-stu-id="b0046-215">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="b0046-216">Bu senaryoda, hiçbir video Hello giriş sahip olduğunda tooforce hello Kodlayıcı tooinsert tek renkli video karşılıklı tooinserting her çıktı bit hızı video olarak yalnızca hello düşük bit hızlı, izlemek isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="b0046-216">In this scenario, when hello input has no video, you may want tooforce hello encoder tooinsert a monochrome video track at just hello lowest bitrate, as opposed tooinserting video at every output bitrate.</span></span> <span data-ttu-id="b0046-217">tooachieve bunu toouse hello gereksinim **InsertBlackIfNoVideoBottomLayerOnly** bayrağı.</span><span class="sxs-lookup"><span data-stu-id="b0046-217">tooachieve this, you need toouse hello **InsertBlackIfNoVideoBottomLayerOnly** flag.</span></span>

<span data-ttu-id="b0046-218">MES hazır belgelenen hello hiçbirini uygulayabileceğiniz [bu](media-services-mes-presets-overview.md) bölümünde ve hello değişikliği yapın:</span><span class="sxs-lookup"><span data-stu-id="b0046-218">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="b0046-219">JSON hazır</span><span class="sxs-lookup"><span data-stu-id="b0046-219">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideoBottomLayerOnly",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="b0046-220">XML hazır</span><span class="sxs-lookup"><span data-stu-id="b0046-220">XML preset</span></span>

<span data-ttu-id="b0046-221">XML, koşul kullanırken bir öznitelik toohello olarak "InsertBlackIfNoVideoBottomLayerOnly" = **H264Video** öğesi ve koşul "InsertSilenceIfNoAudio" öznitelik olarak çok =**AACAudio**.</span><span class="sxs-lookup"><span data-stu-id="b0046-221">When using XML, use Condition="InsertBlackIfNoVideoBottomLayerOnly" as an attribute toohello **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute too**AACAudio**.</span></span>

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

### <a name="inserting-video-at-all-output-bitrates"></a><span data-ttu-id="b0046-222">Bit çıkış video hiç ekleme</span><span class="sxs-lookup"><span data-stu-id="b0046-222">Inserting video at all output bitrates</span></span>
<span data-ttu-id="b0046-223">Bir Çoklu bit hızı gibi önceden kodlama kullanıyorsanız varsayalım ["H264 Çoklu bit hızı 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) bütün giriş video dosyaları ve yalnızca ses dosyaları bir karışımını içeren akış, katalog tooencode.</span><span class="sxs-lookup"><span data-stu-id="b0046-223">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="b0046-224">Bu senaryoda, hiçbir video Hello giriş sahip olduğunda, tek renkli bir video izlemek tüm hello çıkış bit tooforce hello Kodlayıcı tooinsert isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0046-224">In this scenario, when hello input has no video, you may want tooforce hello encoder tooinsert a monochrome video track at all hello output bitrates.</span></span> <span data-ttu-id="b0046-225">Bu, çıktı sağlar varlıklar ile video izler ve ses izleri saygı toonumber tüm homojen.</span><span class="sxs-lookup"><span data-stu-id="b0046-225">This ensures that your output Assets are all homogenous with respect toonumber of video tracks and audio tracks.</span></span> <span data-ttu-id="b0046-226">tooachieve bunu toospecify hello "InsertBlackIfNoVideo" bayrağı gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0046-226">tooachieve this, you need toospecify hello "InsertBlackIfNoVideo" flag.</span></span>

<span data-ttu-id="b0046-227">MES hazır belgelenen hello hiçbirini uygulayabileceğiniz [bu](media-services-mes-presets-overview.md) bölümünde ve hello değişikliği yapın:</span><span class="sxs-lookup"><span data-stu-id="b0046-227">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="b0046-228">JSON hazır</span><span class="sxs-lookup"><span data-stu-id="b0046-228">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideo",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="b0046-229">XML hazır</span><span class="sxs-lookup"><span data-stu-id="b0046-229">XML preset</span></span>

<span data-ttu-id="b0046-230">XML, koşul kullanırken bir öznitelik toohello olarak "InsertBlackIfNoVideo" = **H264Video** öğesi ve koşul "InsertSilenceIfNoAudio" öznitelik olarak çok =**AACAudio**.</span><span class="sxs-lookup"><span data-stu-id="b0046-230">When using XML, use Condition="InsertBlackIfNoVideo" as an attribute toohello **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute too**AACAudio**.</span></span>

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

## <span data-ttu-id="b0046-231"><a id="rotate_video"></a>Bir video Döndür</span><span class="sxs-lookup"><span data-stu-id="b0046-231"><a id="rotate_video"></a>Rotate a video</span></span>
<span data-ttu-id="b0046-232">Merhaba [Medya Kodlayıcısı standart](media-services-dotnet-encode-with-media-encoder-standard.md) 0/90/180/270 açıları tarafından dönüşünü destekler.</span><span class="sxs-lookup"><span data-stu-id="b0046-232">hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 0/90/180/270.</span></span> <span data-ttu-id="b0046-233">"Auto", burada toodetect hello döndürme meta verilerde hello gelen video dosyası çalışır ve için dengelemek Hello varsayılan davranıştır.</span><span class="sxs-lookup"><span data-stu-id="b0046-233">hello default behavior is "Auto", where it tries toodetect hello rotation metadata in hello incoming video file and compensate for it.</span></span> <span data-ttu-id="b0046-234">Merhaba şunlar **kaynakları** öğesi tooone tanımlanan hello hazır [bu](media-services-mes-presets-overview.md) bölümü:</span><span class="sxs-lookup"><span data-stu-id="b0046-234">Include hello following **Sources** element tooone of hello presets defined in [this](media-services-mes-presets-overview.md) section:</span></span>

### <a name="json-preset"></a><span data-ttu-id="b0046-235">JSON hazır</span><span class="sxs-lookup"><span data-stu-id="b0046-235">JSON preset</span></span>
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
### <a name="xml-preset"></a><span data-ttu-id="b0046-236">XML hazır</span><span class="sxs-lookup"><span data-stu-id="b0046-236">XML preset</span></span>
    <Sources>
           <Source>
          <Streams />
          <Filters>
            <Rotation>90</Rotation>
          </Filters>
        </Source>
    </Sources>

<span data-ttu-id="b0046-237">Ayrıca bkz [bu](media-services-mes-schema.md#PreserveResolutionAfterRotation) döndürme maaş tetiklendiğinde konu hello Kodlayıcı hello genişlik ve yükseklik ayarlarında hello yorumlaması hakkında daha fazla bilgi için hazır.</span><span class="sxs-lookup"><span data-stu-id="b0046-237">Also, see [this](media-services-mes-schema.md#PreserveResolutionAfterRotation) topic for more information on how hello encoder interprets hello Width and Height settings in hello preset, when rotation compensation is triggered.</span></span>

<span data-ttu-id="b0046-238">Merhaba "0" değerini tooindicate toohello Kodlayıcı tooignore döndürme meta verileri, varsa hello giriş videoda kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0046-238">You can use hello value "0" tooindicate toohello encoder tooignore rotation metadata, if present, in hello input video.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="b0046-239">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="b0046-239">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b0046-240">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="b0046-240">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="b0046-241">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="b0046-241">See Also</span></span>
[<span data-ttu-id="b0046-242">Media Services kodlama a genel bakış</span><span class="sxs-lookup"><span data-stu-id="b0046-242">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)
