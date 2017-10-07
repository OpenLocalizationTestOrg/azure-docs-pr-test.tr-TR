---
title: "aaaScale medya kullanarak işleme hello Azure portalı | Microsoft Docs"
description: "Bu öğretici hello Azure portal kullanarak işleme ölçeklendirme medya hello adımlarda size yol gösterir."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: e500f733-68aa-450c-b212-cf717c0d15da
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: 89240c6f7579b8795e7b47f2b1c398b1d5477e20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-reserved-unit-type"></a>Merhaba ayrılmış birim türünü değiştir
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [Portal](media-services-portal-scale-media-processing.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>Genel Bakış

Bir Media Services hesabı bir ayrılmış birim görevleri işleme medyanızı işlenme hello hızı belirleyen türü ile ilişkilidir. Merhaba aşağıdaki arasında seçim yapabilirsiniz ayrılmış birim türleri: **S1**, **S2**, veya **S3**. Örneğin, aynı kodlama işi çalıştıktan daha hızlı hello kullandığınızda hello **S2** ayrılmış birim türü karşılaştırma toohello **S1** türü.

Ayrıca toospecifying hello ayrılmış birim türü, hesabınızla tooprovision belirtebilirsiniz **ayrılan birimler** (RUs). sağlanan RUs Hello sayısı belirli bir hesap eşzamanlı olarak işlenebilecek ortam görevleri hello sayısını belirler.

>[!NOTE]
>RU, tüm medya işlemesini paralel hale getirmek için çalışır ve Azure Media Indexer’ın kullanıldığı dizin oluşturma işleri de buna dahildir. Bununla birlikte kodlamadan farklı olarak, dizin oluşturma işleri daha hızlı ayrılmış birimlerde daha hızlı işlenmez.

> [!IMPORTANT]
> Tooreview hello emin olun [genel bakış](media-services-scale-media-processing-overview.md) konu tooget konu işleme medya ölçeklendirme hakkında daha fazla bilgi.
> 
> 

## <a name="scale-media-processing"></a>Medya işlemeyi ölçeklendirme
toochange hello ayrılmış birim türü ve hello ayrılmış birim sayısı, hello aşağıdaki:

1. Merhaba, [Azure portal](https://portal.azure.com/), Azure Media Services hesabınızı seçin.
2. Merhaba, **ayarları** penceresinde, seçin **medya ayrılmış birimleri**.
   
    toochange hello hello için ayrılmış birim sayısı seçilen ayrılmış birim türü, hello kullan **medya sunulan birimleri** kaydırıcı.
   
    toochange hello **AYRILMIŞ birim türü**, S1, S2 ve S3 tuşuna basın.
   
    ![İşlemci sayfası](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. Tuşuna hello düğmesi toosave yaptığınız değişiklikleri KAYDEDİN.
   
    KAYDETME bastığınızda hello yeni ayrılan birimler ayrılır.

## <a name="next-steps"></a>Sonraki adımlar
Media Services öğrenme yollarını gözden geçirin.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

