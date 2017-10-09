---
title: "Medya Kodlayıcısı standart - Azure ile aaaHow toocrop video | Microsoft Docs"
description: "Bu makalede gösterilmektedir nasıl Medya Kodlayıcısı standart ile toocrop video."
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
ms.openlocfilehash: 2b4ac3d96228b93c890a38c57c4913988de1e8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="crop-videos-with-media-encoder-standard"></a><span data-ttu-id="d3295-103">Media Encoder Standard ile videoları kırpma</span><span class="sxs-lookup"><span data-stu-id="d3295-103">Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="d3295-104">Video giriş Medya Kodlayıcısı standart (MES) toocrop kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3295-104">You can use Media Encoder Standard (MES) toocrop your input video.</span></span> <span data-ttu-id="d3295-105">Kırpma hello video çerçevesinde dikdörtgen penceresinin seçilmesi ve yalnızca o penceresinde hello piksel kodlama hello işlemidir.</span><span class="sxs-lookup"><span data-stu-id="d3295-105">Cropping is hello process of selecting a rectangular window within hello video frame, and encoding just hello pixels within that window.</span></span> <span data-ttu-id="d3295-106">Diyagram aşağıdaki hello hello işlem göstermeye yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d3295-106">hello following diagram helps illustrate hello process.</span></span>

![Bir video kırpma](./media/media-services-crop-video/media-services-crop-video01.png)

<span data-ttu-id="d3295-108">Giriş olarak bir çözünürlük 1920 x 1080 piksel (16:9 en boy oranını), ancak etkin video böylece yalnızca 4:3 penceresi veya 1440 x 1080 piksel içerir siyah çubukları (sütun kutuları) hello sol ve sağ içeriyor bir video olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="d3295-108">Suppose you have as input a video that has a resolution of 1920x1080 pixels (16:9 aspect ratio), but has black bars (pillar boxes) at hello left and right, so that only a 4:3 window or 1440x1080 pixels contains active video.</span></span> <span data-ttu-id="d3295-109">MES toocrop kullanın veya hello siyah çubukları düzenleyin ve hello 1440 x 1080 bölge kodlayın.</span><span class="sxs-lookup"><span data-stu-id="d3295-109">You can use MES toocrop or edit out hello black bars, and encode hello 1440x1080 region.</span></span>

<span data-ttu-id="d3295-110">Merhaba kırpma parametrelerini hello kodlama hazır toohello özgün giriş video uygulamak için MES kırpma bir ön-işleme, aşamadır.</span><span class="sxs-lookup"><span data-stu-id="d3295-110">Cropping in MES is a pre-processing stage, so hello cropping parameters in hello encoding preset apply toohello original input video.</span></span> <span data-ttu-id="d3295-111">Bir sonraki aşama kodlamadır ve hello genişliği/yüksekliğinin ayarlarını uygulamak toohello *önceden işlenen* video ve toohello özgün video.</span><span class="sxs-lookup"><span data-stu-id="d3295-111">Encoding is a subsequent stage, and hello width/height settings apply toohello *pre-processed* video, and not toohello original video.</span></span> <span data-ttu-id="d3295-112">Önceden belirlenmiş ayarınız tasarlarken toodo hello aşağıdaki gerekir: (a) hello özgün giriş video dayalı hello kırpma parametreleri ve (b) seçin, video kırpılmış hello üzerinde temel ayarları kodlayın.</span><span class="sxs-lookup"><span data-stu-id="d3295-112">When designing your preset you need toodo hello following: (a) select hello crop parameters based on hello original input video, and (b) select your encode settings based on hello cropped video.</span></span> <span data-ttu-id="d3295-113">Eşleşmiyorsa, video kırpılmış ayarları toohello kodlamak, beklediğiniz gibi hello çıkış olmayacak.</span><span class="sxs-lookup"><span data-stu-id="d3295-113">If you do not match your encode settings toohello cropped video, hello output will not be as you expect.</span></span>

<span data-ttu-id="d3295-114">Merhaba [aşağıdaki](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) konu, kodlama görev toocreate MES kodlama bir işlemle ve nasıl için özel bir toospecify önceden nasıl hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="d3295-114">hello [following](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic shows how toocreate an encoding job with MES and how toospecify a custom preset for hello encoding task.</span></span> 

## <a name="creating-a-custom-preset"></a><span data-ttu-id="d3295-115">Özel bir ön ayarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d3295-115">Creating a custom preset</span></span>
<span data-ttu-id="d3295-116">Merhaba diyagramda gösterildiği hello örnekte:</span><span class="sxs-lookup"><span data-stu-id="d3295-116">In hello example shown in hello diagram:</span></span>

1. <span data-ttu-id="d3295-117">Özgün giriş 1920 x 1080 olabilir</span><span class="sxs-lookup"><span data-stu-id="d3295-117">Original input is 1920x1080</span></span>
2. <span data-ttu-id="d3295-118">Merhaba giriş çerçevede ortalanmış 1440 x 1080, tooan çıktısını kırpılmış toobe gerekiyor</span><span class="sxs-lookup"><span data-stu-id="d3295-118">It needs toobe cropped tooan output of 1440x1080, which is centered in hello input frame</span></span>
3. <span data-ttu-id="d3295-119">Bu (1920 – 1440) X uzaklığını anlamına gelir / 2 = 240 ve bir Y uzaklığı sıfır</span><span class="sxs-lookup"><span data-stu-id="d3295-119">This means an X offset of (1920 – 1440)/2 = 240, and a Y offset of zero</span></span>
4. <span data-ttu-id="d3295-120">Hello genişlik ve yükseklik hello kırpma dikdörtgenin 1440 1080, sırasıyla olduğundan ve</span><span class="sxs-lookup"><span data-stu-id="d3295-120">hello Width and Height of hello Crop rectangle are 1440 and 1080, respectively</span></span>
5. <span data-ttu-id="d3295-121">Hello aşama, hello kodlamak tooproduce üç katmanı olan isteyin, çözümleri 1440 x 1080 960 x 720 ve 480 x 360, sırasıyla olan</span><span class="sxs-lookup"><span data-stu-id="d3295-121">In hello encode stage, hello ask is tooproduce three layers, are resolutions 1440x1080, 960x720 and 480x360, respectively</span></span>

### <a name="json-preset"></a><span data-ttu-id="d3295-122">JSON hazır</span><span class="sxs-lookup"><span data-stu-id="d3295-122">JSON preset</span></span>
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


## <a name="restrictions-on-cropping"></a><span data-ttu-id="d3295-123">Kırpma kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="d3295-123">Restrictions on cropping</span></span>
<span data-ttu-id="d3295-124">özellik kırpma hello toobe el ile amaçlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d3295-124">hello cropping feature is meant toobe manual.</span></span> <span data-ttu-id="d3295-125">Tooload girişinizi video ilgi çerçevelerini seçin, dikdörtgen kırpma hello için hello imleç toodetermine uzaklık konum olanak sağlayan bir uygun düzenleme araç gerekir, toodetermine hello belirli, video, vb. için ayarlanmış kodlama hazır. Bu özellik gibi tooenable şeyleri değildir: otomatik algılama ve video giriş siyah Mektup Kutusu/posta kutusu kenarlıkları kaldırılması.</span><span class="sxs-lookup"><span data-stu-id="d3295-125">You would need tooload your input video into a suitable editing tool that lets you select frames of interest, position hello cursor toodetermine offsets for hello cropping rectangle, toodetermine hello encoding preset that is tuned for that particular video, etc. This feature is not meant tooenable things like: automatic detection and removal of black letterbox/pillarbox borders in your input video.</span></span>

<span data-ttu-id="d3295-126">Özellik kırpma toohello aşağıdaki kısıtlamalar geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d3295-126">Following constraints apply toohello cropping feature.</span></span> <span data-ttu-id="d3295-127">Bunlar karşılanmazsa hello kodlamak görev başarısız veya beklenmeyen bir çıktı üretir.</span><span class="sxs-lookup"><span data-stu-id="d3295-127">If these are not met, hello encode Task can fail, or produce an unexpected output.</span></span>

1. <span data-ttu-id="d3295-128">Merhaba ortak ordinates ve hello kırpma dikdörtgen boyutunu hello giriş video içinde toofit sahip</span><span class="sxs-lookup"><span data-stu-id="d3295-128">hello co-ordinates and size of hello Crop rectangle have toofit within hello input video</span></span>
2. <span data-ttu-id="d3295-129">Yukarıda belirtildiği gibi hello genişliği & hello yüksekliği ayarları kodlamak video kırpılmış toocorrespond toohello sahip</span><span class="sxs-lookup"><span data-stu-id="d3295-129">As mentioned above, hello Width & Height in hello encode settings have toocorrespond toohello cropped video</span></span>
3. <span data-ttu-id="d3295-130">Kırpma yatay modu (dikey olarak tutulan akıllı veya dikey modunda kaydedilen yani uygulanamaz toovideos) yakalanan toovideos uygular</span><span class="sxs-lookup"><span data-stu-id="d3295-130">Cropping applies toovideos captured in landscape mode (i.e. not applicable toovideos recorded with a smartphone held vertically or in portrait mode)</span></span>
4. <span data-ttu-id="d3295-131">Kare piksel ile yakalanan aşamalı video ile en iyi şekilde çalışır</span><span class="sxs-lookup"><span data-stu-id="d3295-131">Works best with progressive video captured with square pixels</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="d3295-132">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="d3295-132">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="d3295-133">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="d3295-133">Next step</span></span>
<span data-ttu-id="d3295-134">Bkz. Azure Media Services öğrenme yolları toohelp AMS tarafından sunulan harika özellikler hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="d3295-134">See Azure Media Services learning paths toohelp you learn about great features offered by AMS.</span></span>  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
