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
# <a name="crop-videos-with-media-encoder-standard"></a>Media Encoder Standard ile videoları kırpma
Video giriş Medya Kodlayıcısı standart (MES) toocrop kullanabilirsiniz. Kırpma hello video çerçevesinde dikdörtgen penceresinin seçilmesi ve yalnızca o penceresinde hello piksel kodlama hello işlemidir. Diyagram aşağıdaki hello hello işlem göstermeye yardımcı olur.

![Bir video kırpma](./media/media-services-crop-video/media-services-crop-video01.png)

Giriş olarak bir çözünürlük 1920 x 1080 piksel (16:9 en boy oranını), ancak etkin video böylece yalnızca 4:3 penceresi veya 1440 x 1080 piksel içerir siyah çubukları (sütun kutuları) hello sol ve sağ içeriyor bir video olduğunu varsayalım. MES toocrop kullanın veya hello siyah çubukları düzenleyin ve hello 1440 x 1080 bölge kodlayın.

Merhaba kırpma parametrelerini hello kodlama hazır toohello özgün giriş video uygulamak için MES kırpma bir ön-işleme, aşamadır. Bir sonraki aşama kodlamadır ve hello genişliği/yüksekliğinin ayarlarını uygulamak toohello *önceden işlenen* video ve toohello özgün video. Önceden belirlenmiş ayarınız tasarlarken toodo hello aşağıdaki gerekir: (a) hello özgün giriş video dayalı hello kırpma parametreleri ve (b) seçin, video kırpılmış hello üzerinde temel ayarları kodlayın. Eşleşmiyorsa, video kırpılmış ayarları toohello kodlamak, beklediğiniz gibi hello çıkış olmayacak.

Merhaba [aşağıdaki](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) konu, kodlama görev toocreate MES kodlama bir işlemle ve nasıl için özel bir toospecify önceden nasıl hello gösterir. 

## <a name="creating-a-custom-preset"></a>Özel bir ön ayarı oluşturma
Merhaba diyagramda gösterildiği hello örnekte:

1. Özgün giriş 1920 x 1080 olabilir
2. Merhaba giriş çerçevede ortalanmış 1440 x 1080, tooan çıktısını kırpılmış toobe gerekiyor
3. Bu (1920 – 1440) X uzaklığını anlamına gelir / 2 = 240 ve bir Y uzaklığı sıfır
4. Hello genişlik ve yükseklik hello kırpma dikdörtgenin 1440 1080, sırasıyla olduğundan ve
5. Hello aşama, hello kodlamak tooproduce üç katmanı olan isteyin, çözümleri 1440 x 1080 960 x 720 ve 480 x 360, sırasıyla olan

### <a name="json-preset"></a>JSON hazır
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


## <a name="restrictions-on-cropping"></a>Kırpma kısıtlamaları
özellik kırpma hello toobe el ile amaçlanmıştır. Tooload girişinizi video ilgi çerçevelerini seçin, dikdörtgen kırpma hello için hello imleç toodetermine uzaklık konum olanak sağlayan bir uygun düzenleme araç gerekir, toodetermine hello belirli, video, vb. için ayarlanmış kodlama hazır. Bu özellik gibi tooenable şeyleri değildir: otomatik algılama ve video giriş siyah Mektup Kutusu/posta kutusu kenarlıkları kaldırılması.

Özellik kırpma toohello aşağıdaki kısıtlamalar geçerlidir. Bunlar karşılanmazsa hello kodlamak görev başarısız veya beklenmeyen bir çıktı üretir.

1. Merhaba ortak ordinates ve hello kırpma dikdörtgen boyutunu hello giriş video içinde toofit sahip
2. Yukarıda belirtildiği gibi hello genişliği & hello yüksekliği ayarları kodlamak video kırpılmış toocorrespond toohello sahip
3. Kırpma yatay modu (dikey olarak tutulan akıllı veya dikey modunda kaydedilen yani uygulanamaz toovideos) yakalanan toovideos uygular
4. Kare piksel ile yakalanan aşamalı video ile en iyi şekilde çalışır

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a>Sonraki adım
Bkz. Azure Media Services öğrenme yolları toohelp AMS tarafından sunulan harika özellikler hakkında bilgi edinin.  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
