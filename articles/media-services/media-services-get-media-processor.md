---
title: "Medya kullanarak işlemci aaaHow tooCreate .NET için Azure Media Services SDK'sı hello | Microsoft Docs"
description: "Nasıl toocreate medya işlemci bileşeni tooencode biçimine dönüştürmek, şifrelemek veya medya içeriği şifresini çözmek için Azure Media Services öğrenin. Kod örnekleri C# dilinde yazılmıştır ve .NET için Media Services SDK'sı hello kullanın."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: dbf9496f-c6f0-42a7-aa36-70f89dcb8ea2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: f133565cc1321d366013f17302adc8bc7585b251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-get-a-media-processor-instance"></a>Nasıl yapılır: bir medya işlemci örneği Al
> [!div class="op_single_selector"]
> * [.NET](media-services-get-media-processor.md)
> * [REST](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a>Genel Bakış
Medya işlemcisi kodlama gibi kodlama, ek olarak, belirli işleme görevi işleyen bir bileşenidir Media Services'de şifreleme veya medya içeriği çözme dönüştürme biçimi. Genellikle bir görev tooencode oluşturulurken medya işlemcisi oluşturma, şifrelemek veya medya içeriği hello biçimine dönüştürün.

## <a name="azure-media-processors"></a>Azure medya işlemcileri 

konu aşağıdaki hello medya işlemcileri listesi sağlar:

* [Kodlama medya işlemcileri](scenarios-and-availability.md#encoding-media-processors)
* [Analizi medya işlemcileri](scenarios-and-availability.md#analytics-media-processors)

## <a name="get-media-processor"></a>Medya işlemcisi Al

yöntem gösterir nasıl aşağıdaki hello tooget medya işlemci örneği. Merhaba kod örneği varsayar adlı bir modül düzeyi değişkeni hello kullanımını **_bağlamı** hello bölümde açıklandığı gibi tooreference hello sunucu bağlamı [nasıl yapılır: Hizmetleri programlamayla tooMedia bağlanmak](media-services-use-aad-auth-to-access-ams-api.md).

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Sonraki Adımlar
Artık bildiğinize göre nasıl tooget medya işlemci örneği Git toohello [nasıl tooEncode bir varlık](media-services-dotnet-encode-with-media-encoder-standard.md) nasıl toouse hello Medya Kodlayıcısı standart tooencode bir varlık gösterecektir konu.

