---
title: "aaaEncode Medya Kodlayıcısı standart ile hello Azure portal kullanarak bir varlık | Microsoft Docs"
description: "Bu öğreticide, Medya Kodlayıcısı standart ile hello Azure portal kullanarak bir varlık kodlama hello adımları açıklanmaktadır."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 107d9e9a-71e9-43e5-b17c-6e00983aceab
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 0d118bbbe1fa9f4ba0bfa3ea3b10fb541d1d6379
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-hello-azure-portal"></a>Medya Kodlayıcısı standart ile hello Azure portal kullanarak bir varlık kodlama
> [!NOTE]
> toocomplete Bu öğretici bir Azure hesabınızın olması gerekir. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

Merhaba en sık karşılaşılan senaryolardan biri, bit hızı Uyarlamalı akış tooyour istemcileri iletmektir Azure Media Services ile çalışırken. Media Services şu bit hızı Uyarlamalı akış teknolojilerini hello destekler: HTTP canlı akışı (HLS), kesintisiz akış, MPEG DASH. tooprepare videolarınızı bit hızı Uyarlamalı akış için tooencode kaynağınız video Çoklu bit hızlı dosyalarıyla gerekir. Merhaba kullanması gereken **Medya Kodlayıcısı standart** Kodlayıcı tooencode videolarınızı.  

Media Services, Çoklu bit hızlı MP4s akış biçimlerine aşağıdaki hello içinde de toodeliver sağlayan dinamik paketleme sağlar: MPEG DASH, HLS, kesintisiz akış, bu akış biçimlerine toore paket kalmadan olmadan. Dinamik paketleme ile toostore yeterlidir ve tek bir depolama biçiminde ve Media Services hello dosyaları ödeme hello istemciden gelen isteklere göre uygun yanıtı derler ve.

tootake avantajı dinamik paketleme, tooencode kaynak dosyanızı Çoklu bit hızlı MP4 dosyaları (kodlama adımları hello gösterilmektedir daha sonra bu bölümde) kümesine ihtiyacınız.

işlem tooscale medya bkz [bu](media-services-portal-scale-media-processing.md) konu.

## <a name="encode-with-hello-azure-portal"></a>Hello Azure portal ile kodlayın
Bu bölüm, içeriğinizi Medya Kodlayıcısı standart ile tooencode uygulayabileceğiniz hello adımları açıklar.

1. Merhaba, [Azure portal](https://portal.azure.com/), Azure Media Services hesabınızı seçin.
2. Merhaba, **ayarları** penceresinde, seçin **varlıklar**.  
3. Merhaba, **varlıklar** penceresinde, select hello varlık tooencode istersiniz.
4. Tuşuna hello **kodla** düğmesi.
5. Merhaba, **bir varlık kodla** penceresi, select hello "Medya Kodlayıcısı standart" işlemcisini ve bir hazır. Hazır ayarlar hakkında daha fazla bilgi için bkz. [Bit hızı merdivenini otomatik oluşturma](media-services-autogen-bitrate-ladder-with-mes.md) ve [MES Görev Ön Ayarları](media-services-mes-presets-overview.md). Hangi kodlama hazır kullanılır toocontrol planlıyorsanız, bunu göz önünde bulundurun: tooselect hello giriş videonuzun için en uygun olan Önayar önemlidir. Giriş videonuzun 1920 x 1080 piksel çözünürlüğü sahip biliyorsanız, örneğin, hello kullanabilirsiniz "H264 Çoklu bit hızı 1080p" hazır. Düşük çözünürlüklü (640 x 360) bir videonuz olması durumunda "H264 Çoklu Bit hızı 1080p" ön ayarını kullanmamalısınız.
   
   Daha kolay yönetim için hello hello çıkış varlık adını düzenleme ve hello işinin hello adı bir seçeneğiniz vardır.
   
   ![Varlıkları kodlama](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. **Oluştur**’a basın.

## <a name="next-step"></a>Sonraki adım
Bölümünde açıklandığı gibi hello Azure portal ile kodlama işi ilerleme durumunu izleyebilirsiniz [bu](media-services-portal-check-job-progress.md) makalesi.  

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

