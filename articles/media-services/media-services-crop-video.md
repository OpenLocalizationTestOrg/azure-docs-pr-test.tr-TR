---
title: "Medya Kodlayıcısı standart - Azure ile video kırpma | Microsoft Docs"
description: "Bu makalede, Medya Kodlayıcısı standart ile video kırpma gösterilmektedir."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 7628f674-2005-4531-8b61-d7a4f53e46ba
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/09/2017
ms.author: anilmur;juliako;
ms.openlocfilehash: 60d0ce14a271fcbe698559da95ca011cb888b221
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="crop-videos-with-media-encoder-standard"></a><span data-ttu-id="13f79-103">Media Encoder Standard ile videoları kırpma</span><span class="sxs-lookup"><span data-stu-id="13f79-103">Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="13f79-104">Giriş video kırpma için Medya Kodlayıcısı standart (MES) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13f79-104">You can use Media Encoder Standard (MES) to crop your input video.</span></span> <span data-ttu-id="13f79-105">Kırpma video çerçevesinde dikdörtgen penceresinin seçilmesi ve yalnızca o penceresi içinde piksel kodlama işlemidir.</span><span class="sxs-lookup"><span data-stu-id="13f79-105">Cropping is the process of selecting a rectangular window within the video frame, and encoding just the pixels within that window.</span></span> <span data-ttu-id="13f79-106">Aşağıdaki diyagramda, işlem göstermeye yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="13f79-106">The following diagram helps illustrate the process.</span></span>

![Bir video kırpma](./media/media-services-crop-video/media-services-crop-video01.png)

<span data-ttu-id="13f79-108">Yalnızca 4:3 penceresi veya 1440 x 1080 piksel içeren etkin video böylece çözünürlük 1920 x 1080 piksel (16:9 en boy oranını) olsa da, sol ve sağ tarafta, siyah çubukları (sütun kutuları) sahip bir video giriş olarak olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="13f79-108">Suppose you have as input a video that has a resolution of 1920x1080 pixels (16:9 aspect ratio), but has black bars (pillar boxes) at the left and right, so that only a 4:3 window or 1440x1080 pixels contains active video.</span></span> <span data-ttu-id="13f79-109">1440 x 1080 bölge kodlamak ve MES kırpma veya siyah çubuklar düzenlemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="13f79-109">You can use MES to crop or edit out the black bars, and encode the 1440x1080 region.</span></span>

<span data-ttu-id="13f79-110">Kodlama hazır kırpma parametreleri özgün giriş videoya uygulamak için MES kırpma bir ön-işleme, aşamadır.</span><span class="sxs-lookup"><span data-stu-id="13f79-110">Cropping in MES is a pre-processing stage, so the cropping parameters in the encoding preset apply to the original input video.</span></span> <span data-ttu-id="13f79-111">Bir sonraki aşama kodlamadır ve genişliği/yüksekliğinin ayarlarının uygulanacağı *önceden işlenen* video ve özgün video uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="13f79-111">Encoding is a subsequent stage, and the width/height settings apply to the *pre-processed* video, and not to the original video.</span></span> <span data-ttu-id="13f79-112">Önceden belirlenmiş ayarınız tasarlarken, aşağıdakileri yapmanız gerekir: (a) özgün giriş video dayalı kırpma parametreleri seçin ve (b) seçin, kırpılmış video dayalı ayarları kodlayın.</span><span class="sxs-lookup"><span data-stu-id="13f79-112">When designing your preset you need to do the following: (a) select the crop parameters based on the original input video, and (b) select your encode settings based on the cropped video.</span></span> <span data-ttu-id="13f79-113">Eşleşmiyorsa, kırpılmış video ayarlar kodlamak, beklediğiniz gibi çıkış olmaz.</span><span class="sxs-lookup"><span data-stu-id="13f79-113">If you do not match your encode settings to the cropped video, the output will not be as you expect.</span></span>

<span data-ttu-id="13f79-114">[Aşağıdaki](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) konu ile MES bir kodlama işi oluşturma ve kodlama görev için önceden belirlenmiş bir özel belirtme gösterir.</span><span class="sxs-lookup"><span data-stu-id="13f79-114">The [following](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic shows how to create an encoding job with MES and how to specify a custom preset for the encoding task.</span></span> 

## <a name="creating-a-custom-preset"></a><span data-ttu-id="13f79-115">Özel bir ön ayarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="13f79-115">Creating a custom preset</span></span>
<span data-ttu-id="13f79-116">Aşağıdaki çizimde gösterilen örnekte:</span><span class="sxs-lookup"><span data-stu-id="13f79-116">In the example shown in the diagram:</span></span>

1. <span data-ttu-id="13f79-117">Özgün giriş 1920 x 1080 olabilir</span><span class="sxs-lookup"><span data-stu-id="13f79-117">Original input is 1920x1080</span></span>
2. <span data-ttu-id="13f79-118">Giriş çerçevede ortalanmış 1440 x 1080, çıktısı kırpılmış gerekir</span><span class="sxs-lookup"><span data-stu-id="13f79-118">It needs to be cropped to an output of 1440x1080, which is centered in the input frame</span></span>
3. <span data-ttu-id="13f79-119">Bu (1920 – 1440) X uzaklığını anlamına gelir / 2 = 240 ve bir Y uzaklığı sıfır</span><span class="sxs-lookup"><span data-stu-id="13f79-119">This means an X offset of (1920 – 1440)/2 = 240, and a Y offset of zero</span></span>
4. <span data-ttu-id="13f79-120">Genişlik ve yükseklik kırpma dikdörtgenin 1440 ve 1080, sırasıyla olan</span><span class="sxs-lookup"><span data-stu-id="13f79-120">The Width and Height of the Crop rectangle are 1440 and 1080, respectively</span></span>
5. <span data-ttu-id="13f79-121">Kodla aşamasında sor üç katmanı oluşturmak için bu çözümleri 1440 x 1080 960 x 720 ve 480 x 360, sırasıyla olan</span><span class="sxs-lookup"><span data-stu-id="13f79-121">In the encode stage, the ask is to produce three layers, are resolutions 1440x1080, 960x720 and 480x360, respectively</span></span>

### <a name="json-preset"></a><span data-ttu-id="13f79-122">JSON hazır</span><span class="sxs-lookup"><span data-stu-id="13f79-122">JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "Crop": {
                "X": 240,
                "Y": 0,
                "Width": 1440,
                "Height": 1080
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
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1440,
              "Height": 1080,
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
              "Bitrate": 1250,
              "MaxBitrate": 1250,
              "BufferWindow": "00:00:05",
              "Width": 480,
              "Height": 360,
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


## <a name="restrictions-on-cropping"></a><span data-ttu-id="13f79-123">Kırpma kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="13f79-123">Restrictions on cropping</span></span>
<span data-ttu-id="13f79-124">Kırpma özelliği el ile olması amaçlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="13f79-124">The cropping feature is meant to be manual.</span></span> <span data-ttu-id="13f79-125">Giriş videonuzun, ilgi çerçevelerini seçin, bu belirli video, vb. için ayarlanmış kodlama hazır belirlemek için kırpma dikdörtgeninin için uzaklık belirlemek için imleç Konumlandır sağlar uygun bir düzenleme aracı yüklemek için gerekir. Bu özellik gibi şeyleri etkinleştirmek üzere tasarlanmamıştır: otomatik algılama ve video giriş siyah Mektup Kutusu/posta kutusu kenarlıkları kaldırılması.</span><span class="sxs-lookup"><span data-stu-id="13f79-125">You would need to load your input video into a suitable editing tool that lets you select frames of interest, position the cursor to determine offsets for the cropping rectangle, to determine the encoding preset that is tuned for that particular video, etc. This feature is not meant to enable things like: automatic detection and removal of black letterbox/pillarbox borders in your input video.</span></span>

<span data-ttu-id="13f79-126">Aşağıdaki kısıtlamalar kırpma özelliği için geçerli.</span><span class="sxs-lookup"><span data-stu-id="13f79-126">Following constraints apply to the cropping feature.</span></span> <span data-ttu-id="13f79-127">Bunlar karşılanmazsa görev kodla başarısız veya beklenmeyen bir çıktı oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="13f79-127">If these are not met, the encode Task can fail, or produce an unexpected output.</span></span>

1. <span data-ttu-id="13f79-128">Ortak ordinates ve kırpma dikdörtgen boyutunu içinde giriş video uyması gerekir</span><span class="sxs-lookup"><span data-stu-id="13f79-128">The co-ordinates and size of the Crop rectangle have to fit within the input video</span></span>
2. <span data-ttu-id="13f79-129">Yukarıda belirtildiği gibi genişliğini ve yüksekliğini kodla ayarlarında kırpılmış videoya karşılık gerekir</span><span class="sxs-lookup"><span data-stu-id="13f79-129">As mentioned above, the Width & Height in the encode settings have to correspond to the cropped video</span></span>
3. <span data-ttu-id="13f79-130">Kırpma yatay modunda yakalanan videolar için geçerlidir (yani dikey veya dikey modunda smartphone ile kaydedilen videolar uygulanamaz tutulan)</span><span class="sxs-lookup"><span data-stu-id="13f79-130">Cropping applies to videos captured in landscape mode (i.e. not applicable to videos recorded with a smartphone held vertically or in portrait mode)</span></span>
4. <span data-ttu-id="13f79-131">Kare piksel ile yakalanan aşamalı video ile en iyi şekilde çalışır</span><span class="sxs-lookup"><span data-stu-id="13f79-131">Works best with progressive video captured with square pixels</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="13f79-132">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="13f79-132">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="13f79-133">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="13f79-133">Next step</span></span>
<span data-ttu-id="13f79-134">AMS tarafından sunulan harika özellikler hakkında bilgi edinmenize yardımcı olmak üzere Azure Media Services'i öğrenme yolları bakın.</span><span class="sxs-lookup"><span data-stu-id="13f79-134">See Azure Media Services learning paths to help you learn about great features offered by AMS.</span></span>  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
