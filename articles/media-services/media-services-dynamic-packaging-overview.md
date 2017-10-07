---
title: "aaaAzure Media Services dinamik paketleme genel bakış | Microsoft Docs"
description: "Merhaba konu sağlar ve dinamik paketleme genel bakış."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0d9e4f54-5daa-45c1-bfaa-cf09ca89b812
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 970e24eba800e098774172c87f56629430b227a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-packaging"></a>Dinamik paketleme
## <a name="overview"></a>Genel Bakış
Microsoft Azure Media Services, kullanılan toodeliver olabilir birçok medya kaynak dosya biçimleri, medya akış biçimlerine ve içerik koruma biçimleri tooa istemci teknolojileri çeşitli (örneğin, iOS, XBOX, Silverlight, Windows 8). Bu istemciler farklı protokollere anlamanıza, örneğin bir HTTP canlı akışı (HLS) V4 biçiminde iOS gerektirir ve Silverlight ve Xbox kesintisiz akış gerektirir. Uyarlamalı bit hızlı (Çoklu bit hızı) kümesi varsa MP4 (ISO temel medya 14496-12) dosyaları veya uyarlamalı bit hızlı kesintisiz akış dosyalarının MPEG DASH, HLS veya kesintisiz akış anlamak tooserve tooclients istediğiniz kümesi, medya avantajlarından almalıdır Dinamik paketleme Hizmetleri.

Dinamik tüm yapmanız gereken paketleme ile toocreate Uyarlamalı bit hızlı MP4 veya uyarlamalı bit hızlı kesintisiz akış dosyaları kümesi içeren bir varlıktır. Merhaba hello bildiriminde belirtilen biçime bağlı olarak veya istek parçalara, hello isteğe bağlı Akış sunucusu, hello akış seçmiş olduğunuz hello protokolde almanızı sağlar. Sonuç olarak, yalnızca toostore gerekir ve tek bir depolama biçiminde ve Media Services hizmeti hello dosyaları ödeme hello istemciden gelen isteklere göre uygun yanıtı derler ve.

Merhaba Aşağıdaki diyagramda hello geleneksel kodlama ve statik paketleme iş akışı gösterilmektedir.

![Statik kodlama](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

Merhaba Aşağıdaki diyagramda hello dinamik paketleme iş akışı gösterilmektedir.

![Dinamik kodlama](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a>Yaygın bir senaryo
1. (Bir ara dosyayı olarak adlandırılır) bir giriş dosyasını karşıya yükleyin. Örneğin, H.264, MP4 veya WMV (desteklenen biçimler hello listesi için bkz [hello Medya Kodlayıcısı standart tarafından desteklenen biçimleri](media-services-media-encoder-standard-formats.md).
2. Mezzanine dosya tooH.264 MP4 bit hızı Uyarlamalı kümelerinizi kodlayın.
3. Merhaba isteğe bağlı Bulucu oluşturarak hello Uyarlamalı bit hızı MP4 kümesine içeren hello varlığı yayımlayın.
4. URL'leri tooaccess akış hello oluşturun ve, içerik akışı sağlama.

## <a name="preparing-assets-for-dynamic-streaming"></a>Varlıklar dinamik akış için hazırlama
tooprepare varlığınız, akış dinamik için iki seçenek vardır:

1. [Ana dosya karşıya yükleme](media-services-dotnet-upload-files.md).
2. [Merhaba Medya Kodlayıcısı standart Kodlayıcı tooproduce H.264 MP4 bit hızı Uyarlamalı kümeleri kullanan](media-services-dotnet-encode-with-media-encoder-standard.md).
3. [Kullanıcınıza içeriğinizin akışını](media-services-deliver-content-overview.md).

## <a id="unsupported_formats"></a>Dinamik paketleme tarafından desteklenmeyen biçimleri
Merhaba aşağıdaki kaynak dosya biçimlerini dinamik paketleme tarafından desteklenmez.

* Dolby dijital mp4 dosyaları.
* Dolby dijital kesintisiz dosyalar.

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

