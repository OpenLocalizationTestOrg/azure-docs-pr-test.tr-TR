---
title: "aaaTask hazır MES (Medya Kodlayıcısı standart) için | Microsoft Docs"
description: "Merhaba konu sağlar ve görev hazır MES (Medya Kodlayıcısı standart) için genel bakış."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: f243ed1c-ac9c-4300-a5f7-f092cf9853b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 56e098d6d8c8f84031421ec59f087f20370ba111
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="task-presets-for-mes-media-encoder-standard"></a>Görev hazır MES (Medya Kodlayıcısı standart) için

**Medya Kodlayıcısı standart** kodlama işler oluştururken kullanabileceğiniz hazır kodlama kümesi tanımlar. Toouse hello "Uyarlamalı Media Services ile akış için tooencode video istiyorsanız önceden akış" önerilir. Bu önceden belirlenmiş, Medya Kodlayıcısı standart işlem belirttiğinizde [bit hızı Merdiveni otomatik oluşturma](media-services-autogen-bitrate-ladder-with-mes.md). 

Ancak, toocustomize bir kodlama hazır ihtiyacınız varsa, bu bölümde, özel yapılandırma için bir şablon olarak tanımlanan hazır kodlama hello sürer. Merhaba hangi her bir öğe bu hazır anlamına gelir ve hello geçerli değerlerin her öğe için açıklamalar için bkz: [Medya Kodlayıcısı standart şema](media-services-mes-schema.md) konu.  
  
> [!NOTE]
>  4 k kodlar için bir hazır kullanırken, hello almalısınız `S3` ayrılmış birim türü. Daha fazla bilgi için bkz: [nasıl tooScale kodlama](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).  
  
Medya Kodlayıcısı standart ile çalışırken, döndürme varsayılan olarak etkindir. Videonuzu akıllı veya diğer mobil cihaz dikey modunda kayıtlı değilse, ardından bu hazır ayarları varsayılan olarak, bunları tooLandscape modu önceki tooencoding (aksine, video döndürme işlemini el ile bir işlem olduğu Azure medya Kodlayıcı ile çalışırken döndürüleceğini açıklandığı gibi [bu](http://azure.microsoft.com/blog/2014/08/21/advanced-encoding-features-in-azure-media-encoder/) "Video döndürme" altında blog).  
  
Kullanılabilir hazır ayarlar:  
  
 [H264 Çoklu bit hızı 1080p ses 5.1](media-services-mes-preset-H264-Multiple-Bitrate-1080p-Audio-5.1.md) 6000 kbps too400 kbps ve AAC 5.1 ses 8 GOP hizalı MP4 dosyaları kümesi üretir.  
  
 [H264 Çoklu bit hızı 1080p](media-services-mes-preset-H264-Multiple-Bitrate-1080p.md) 6000 kbps too400 kbps ve stereo AAC ses 8 GOP hizalı MP4 dosyaları kümesi üretir.  
  
 [H264 Çoklu bit hızı 16 x 9 iOS için](media-services-mes-preset-H264-Multiple-Bitrate-16x9-for-iOS.md) 8500 kbps too200 kbps ve stereo AAC ses 8 GOP hizalı MP4 dosyaları kümesi üretir.  
  
 [H264 Çoklu bit hızı 16 x 9 SD ses 5.1](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD-Audio-5.1.md) 1900 kbps too400 kbps ve AAC 5.1 ses 5 GOP hizalı MP4 dosyaları kümesi üretir.  
  
 [H264 Çoklu bit hızı 16 x 9 SD](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD.md) 1900 kbps too400 kbps ve stereo AAC ses 5 GOP hizalı MP4 dosyaları kümesi üretir.  
  
 [H264 Çoklu bit hızı 4K ses 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4K-Audio-5.1.md) 20000 kbps too1000 kbps ve AAC 5.1 ses 12 GOP hizalı MP4 dosyaları kümesi üretir.  
  
 [H264 Çoklu bit hızı 4K](media-services-mes-preset-H264-Multiple-Bitrate-4K.md) 20000 kbps too1000 kbps ve stereo AAC ses 12 GOP hizalı MP4 dosyaları kümesi üretir.  
  
 [H264 Çoklu bit hızı 4 x 3 iOS için](media-services-mes-preset-H264-Multiple-Bitrate-4x3-for-iOS.md) 8500 kbps too200 kbps ve stereo AAC ses 8 GOP hizalı MP4 dosyaları kümesi üretir.  
  
 [H264 Çoklu bit hızı 4 x 3 SD ses 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD-Audio-5.1.md) 1600 kbps too400 kbps ve AAC 5.1 ses 5 GOP hizalı MP4 dosyaları kümesi üretir.  
  
 [H264 Çoklu bit hızı 4 x 3 SD](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD.md) 1600 kbps too400 kbps ve stereo AAC ses 5 GOP hizalı MP4 dosyaları kümesi üretir.  
  
 [H264 Çoklu bit hızı 720p ses 5.1](media-services-mes-preset-H264-Multiple-Bitrate-720p-Audio-5.1.md) 3400 kbps too400 kbps ve AAC 5.1 ses 6 GOP hizalı MP4 dosyaları kümesi üretir.  
  
 [H264 Çoklu bit hızı 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) 3400 kbps too400 kbps ve stereo AAC ses 6 GOP hizalı MP4 dosyaları kümesi üretir.  
  
 [H264 Çoklu bit hızı 1080p ses 5.1](media-services-mes-preset-H264-Single-Bitrate-1080p-Audio-5.1.md) 6750 kbps ve AAC 5.1 ses bit hızı ile tek bir MP4 dosyası oluşturur.  
  
 [H264 Çoklu bit hızı 1080p](media-services-mes-preset-H264-Single-Bitrate-1080p.md) 6750 kbps stereo AAC ses ve bit hızı ile tek bir MP4 dosyası oluşturur.  
  
 [H264 Çoklu bit hızı 4K ses 5.1](media-services-mes-preset-H264-Single-Bitrate-4K-Audio-5.1.md) 18000 kbps ve AAC 5.1 ses bit hızı ile tek bir MP4 dosyası oluşturur.  
  
 [H264 Çoklu bit hızı 4K](media-services-mes-preset-H264-Single-Bitrate-4K.md) 18000 kbps stereo AAC ses ve bit hızı ile tek bir MP4 dosyası oluşturur.  
  
 [H264 Çoklu bit hızı 4 x 3 SD ses 5.1](media-services-mes-preset-H264-Single-Bitrate-4x3-SD-Audio-5.1.md) 1800 kbps ve AAC 5.1 ses bit hızı ile tek bir MP4 dosyası oluşturur.  
  
 [H264 Çoklu bit hızı 4 x 3 SD](media-services-mes-preset-H264-Single-Bitrate-4x3-SD.md) 1800 kbps stereo AAC ses ve bit hızı ile tek bir MP4 dosyası oluşturur.  
  
 [H264 Çoklu bit hızı 16 x 9 SD ses 5.1](media-services-mes-preset-H264-Single-Bitrate-16x9-SD-Audio-5.1.md) 2200 kbps ve AAC 5.1 ses bit hızı ile tek bir MP4 dosyası oluşturur.  
  
 [H264 Çoklu bit hızı 16 x 9 SD](media-services-mes-preset-H264-Single-Bitrate-16x9-SD.md) 2200 kbps stereo AAC ses ve bit hızı ile tek bir MP4 dosyası oluşturur.  
  
 [H264 Çoklu bit hızı 720p ses 5.1](media-services-mes-preset-H264-Single-Bitrate-720p-Audio-5.1.md) 4500 kbps ve AAC 5.1 ses bit hızı ile tek bir MP4 dosyası oluşturur.  
  
 [H264 Çoklu bit hızı Android 720p](media-services-mes-preset-H264-Single-Bitrate-720p-for-Android.md) hazır bir bit hızı 2000 kbps ve stereo AAC ile tek bir MP4 dosyası oluşturur.  
  
 [H264 Çoklu bit hızı 720p](media-services-mes-preset-H264-Single-Bitrate-720p.md) 4500 kbps stereo AAC ses ve bit hızı ile tek bir MP4 dosyası oluşturur.  
  
 [H264 Çoklu bit hızı yüksek kaliteli SD Android için](media-services-mes-preset-H264-Single-Bitrate-High-Quality-SD-for-Android.md) 500 Kb/sn ve stereo AAC ses bit hızı ile tek bir MP4 dosyası üreten...  
  
 [H264 Çoklu bit hızı düşük kalite SD Android için](media-services-mes-preset-H264-Single-Bitrate-Low-Quality-SD-for-Android.md) 56 kbps stereo AAC ses ve bit hızı ile tek bir MP4 dosyası oluşturur.  
  
 Daha fazla bilgi için bkz: ilgili tooMedia Hizmetleri kodlayıcılar [kodlama isteğe bağlı Azure Media Services ile](https://azure.microsoft.com/en-us/documentation/articles/media-services-encode-asset/).
