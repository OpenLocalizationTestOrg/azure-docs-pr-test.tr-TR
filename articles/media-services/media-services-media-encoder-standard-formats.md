---
title: "aaaMedia Kodlayıcısı standart biçimleri ve codec bileşenleri"
description: "Bu konuda Medya Kodlayıcısı standart biçimleri ve codec bileşenleri genel bakış sağlar."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: f334b1ce-2f56-4968-a019-f0a2b0016d9f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 51a67f372dff579383ffcfa988e8f4d38ad44a72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="media-encoder-standard-formats-and-codecs"></a>Media Encoder Standard Biçimleri ve Kodlayıcılar
Bu belge hello en yaygın alma ve Medya Kodlayıcısı standart ile kullanabileceğiniz dışa aktarma dosyası biçimi listesini içerir.

## <a name="input-containerfile-formats"></a>Kapsayıcı/dosya biçimleri giriş
| Dosya biçimleri (dosya uzantıları) | Destekleniyor |
| --- | --- | --- | --- |
| (İle H.264 ve AAC codec bileşenleri) FLV (.flv) |Evet |
| MXF (.mxf) |Evet |
| GXF (.gxf) |Evet |
| MPEG2 PS, MPEG2-TS 3GP (.ts, .ps, .3gp, .3gpp, .mpg) |Evet |
| Windows Media Video (WMV) / ASF (.wmv, .asf) |Evet |
| AVI (sıkıştırılmamış 8 bit/10 bit) (.avi) |Evet |
| MP4 (.mp4, .m4a, .m4v) / ISMV (.isma, .ismv) |Evet |
| [Microsoft Dijital Video Recording(DVR-MS)](https://msdn.microsoft.com/library/windows/desktop/dd692984) (.dvr-ms) |Evet |
| Matroska/WebM (.mkv) |Evet |
| WAVE/WAV (.wav) |Evet |
| QuickTime (.mov) |Evet |

> [!NOTE]
> Yukarıdaki daha sık karşılaşılan hello dosya uzantıları listesini içerir. Medya Kodlayıcısı standart destek diğer birçok (örneğin: .m2ts, .mpeg2video, .qt). Lütfen tooencode bir dosya deneyin ve hello biçimi desteklenmiyor ilgili bir hata iletisi alırsanız bir geri bildirim sağlamak [burada](https://feedback.azure.com/forums/169396-media-services/category/144411-encoding-and-processing/).
> 
> 

### <a name="audio-formats-in-input-containers"></a>Giriş kapsayıcılarında ses biçimleri
Medya Kodlayıcısı standart giriş kapsayıcılarında ses biçimleri aşağıdaki taşıma hello destekler:

* MXF, GXF ve QuickTime dosyaları araya eklemeli stereo ile ses izleri veya 5.1 örnekleri olan

or

* Burada hello ses yazımının ayrı PCM izler ancak hello kanal eşleme olarak MXF, GXF ve QuickTime dosyaları (toostereo veya 5.1) hello dosya meta verilerini anlaşılan

Açık/kullanıcı tarafından sağlanan kanal eşleme hello yakın gelecekte sağlanacak için destekleyen unutmayın.

## <a name="input-video-codecs"></a>Görüntü codec bileşenleri giriş
| Görüntü codec bileşenleri giriş | Destekleniyor |
| --- | --- | --- | --- |
| AVC 8 bit/10-bit too4:2:2 AVCIntra dahil olmak üzere, ayarlama |8 bit 4:2:0. ve 4:2:2 |
| Hırslı DNxHD (içinde MXF) |Evet |
| DVCPro/DVCProHD (içinde MXF) |Evet |
| Dijital video (DV) (AVI dosyaları) |Evet |
| JPEG 2000 |Evet |
| MPEG-2 (too422 profili ve yüksek düzey; XDCAM, XDCAM HD, XDCAM IMX, CableLabs® ve D10 gibi çeşitleri dahil) |Too422 profili |
| MPEG-1 |Evet |
| VC-1/WMV9 |Evet |
| Canopus denetim merkezini/HQX |Hayır |
| MPEG-4 bölüm 2 |Evet |
| [Theora](https://en.wikipedia.org/wiki/Theora) |Evet |
| Sıkıştırılmamış YUV420 veya Ara |Evet |
| Apple ProRes 422 |Evet |
| Apple ProRes 422 LT |Evet |
| Apple ProRes 422 denetim merkezini |Evet |
| Apple ProRes Proxy |Evet |
| Apple ProRes 4444 |Evet |
| Apple ProRes 4444 XQ |Evet |

## <a name="input-audio-codecs"></a>Giriş ses codec bileşenleri
| Giriş ses codec bileşenleri | Destekleniyor |
| --- | --- | --- | --- |
| AAC (AAC-LC, HE AAC ve AAC-HEv2; too5.1 yukarı) |Evet |
| MPEG Katman 2 |Evet |
| MP3 (MPEG-1 ses Katman 3) |Evet |
| Windows Media Ses |Evet |
| WAV/PCM |Evet |
| [FLAC](https://en.wikipedia.org/wiki/FLAC)</a> |Evet |
| [Geçerli](http://go.microsoft.com/fwlink/?LinkId=822667) |Evet |
| [Vorbis](https://en.wikipedia.org/wiki/Vorbis)</a> |Evet |
| AMR (Uyarlamalı çok hızı) |Evet |
| AES (SMPTE 331 M ve 302 M, AES3 2003) |Hayır |
| Dolby® E |Hayır |
| Dolby® dijital (AC3) |Hayır |
| Dolby® dijital artı (E-AC3) |Hayır |

## <a name="output-formats-and-codecs"></a>Çıktı biçimi ve codec bileşenleri
Aşağıdaki tablonun hello dışa aktarmak için desteklenen hello codec bileşenleri ve dosya biçimlerini listeler.

| Dosya biçimi | Görüntü Codec | Ses Codec |
| --- | --- | --- |
| MP4 <br/><br/>(Çoklu bit hızlı MP4 kapsayıcıları dahil) |H.264 (yüksek, ana ve temel profilleri) |AAC-LC, HE-AAC v1, HE-AAC v2 |
| MPEG2 TS |H.264 (yüksek, ana ve temel profilleri) |AAC-LC, HE-AAC v1, HE-AAC v2 |

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Ayrıca bkz.
[Azure Media Services ile isteğe bağlı içerik kodlama](media-services-encode-asset.md)

[Nasıl tooencode Medya Kodlayıcısı standart ile](media-services-dotnet-encode-with-media-encoder-standard.md)

