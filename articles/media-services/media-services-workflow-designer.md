---
title: "Gelişmiş kodlama iş akışı Tasarımcısı ile aaaCreate | Microsoft Docs"
description: "İş Akışı Tasarımcısı kodlama iş akışlarıyla nasıl toocreate Gelişmiş hakkında bilgi edinin."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 004815f2-0761-4706-87a1-675ba36e0322
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako;johndeu;anilmur
ms.openlocfilehash: 3744cde54c78bec7c7b586962ec1a8fe9529c1d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-advanced-encoding-workflows-with-workflow-designer"></a>İş Akışı Tasarımcısı ile Gelişmiş Kodlama İş Akışları Oluşturma
## <a name="overview"></a>Genel Bakış
Merhaba **iş akışı Tasarımcısı** ile kodlamak için kullanılan toodesign ve yapı özel iş akışları bir Windows Masaüstü araç **Medya Kodlayıcısı Premium iş akışı**.
Hello gücünü hello iş akışı Tasarımcısı aracını kullanarak, tasarım ve çalışacak karmaşık iş akışları oluşturmak **Medya Kodlayıcısı Premium**.  

İş akışları müşteri karar mantık içerebilir ve dallara ayırma hello giriş kaynağı dosyanın özelliklerine bağlı. Geçersiz kılınabilir özellikleri ve dinamik değerler toomake bile hello en karmaşık kodlama görevleri kolay toorepeat iş akışları oluşturmak ve hello bulutta özelleştirebilirsiniz.

Oluşturabileceğiniz örnek iş akışları içerir:

* Karar hello kaynak içerik çözümlemesi için inceleyebilir ve yalnızca hello istenen çıkış parçaları kodlamak iş akışları temel.  Merhaba kaynak içerik inadvertantly upscaling tarafından oluşturulacak küçülttüğü iyi bir şekilde hello parçaları ortadan kaldırarak helfpul budur.
* Birden çok giriş dosyaları kullanılan toosupport başlıklar, yer paylaşımları ve Dikiş birlikte içeriği olabilir. 

Bu araç ayrıca kullanılan toomodify herhangi biri olabilir bizim [iş akışları yayımlanan](media-services-workflow-designer.md#existing_workflows). 

> [!NOTE]
> tooget hello iş akışı Tasarımcısı aracını kopyanızı temasa mepd@microsoft.com.
> 
> 

Bir iş akışı dosyası oluşturulduktan sonra bir varlık yüklenebilir ve daha sonra medya dosyalarını kodlama için kullanılıyor. Hakkında bilgi için tooencode ile **Medya Kodlayıcısı Premium iş akışı** kullanarak **.NET**, bkz: [Medya Kodlayıcısı Premium akışıyla kodlama Gelişmiş](media-services-encode-with-premium-workflow.md).

## <a id="existing_workflows"></a>Var olan iş akışlarını değiştirin
Merhaba varsayılan [iş akışları yayımlanan](media-services-workflow-designer.md#existing_workflows) hello Tasarımcı aracı kullanılarak değiştirilebilir. Merhaba varsayılan iş akışı dosyalarını almak [burada](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows). Başlangıç klasörü de bu dosyaları hello açıklamasını içerir.

videoları izleyerek hello nasıl toouse hello Tasarımcısı göstermektedir.

### <a name="day-1--getting-started"></a>Günde 1 – Başlarken
Günde 1 video kapsar:

* Tasarımcı genel bakış
* Temel iş akışları – "Hello World"
* Çıkış MP4 dosyaları Azure Media Services akış ile kullanım için birden çok oluşturma

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Premium-Encoder-Workflow-Designer-Training-Videos-Day-1/player]
> 
> 

### <a name="day-2"></a>Gün 2
Gün 2 video kapsar:

* Kaynak dosya senaryoları değişen – ses işleme
* Gelişmiş mantığı ile iş akışları
* Grafik aşamaları

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Premium-Encoder-Workflow-Designer-Training-Videos-Day-2/player]
> 
> 

### <a name="day-3"></a>Gün 3
Gün 3 video kapsar:

* İş akışları/planlar içinde komut dosyası oluşturma
* Geçerli Kodlayıcı kısıtlamalarıyla hello
* SORU- CEVAP

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Premium-Encoder-Workflow-Designer-Training-Videos-Day-3/player]
> 
> 

## <a name="next-step"></a>Sonraki adım
Media Services öğrenme yollarını gözden geçirin.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

Destek veya hello iş akışı Tasarımcısı aracında özel iş akışları oluşturma hakkında sorularınız varsa lütfen e-posta gönderin toomepd@microsoft.com.

## <a name="see-also"></a>Ayrıca Bkz.
[Azure Premium Kodlayıcı iş akışı Tasarımcısı eğitim videoları](http://johndeutscher.com/2015/07/06/azure-premium-encoder-workflow-designer-training-videos/)

