---
title: "AAA Yönet hızı ve Azure Media Services ile kodlama eşzamanlılık | Microsoft Docs"
description: "Bu makalede hızı ve Azure Media Services ile kodlama işleri/görevleri eşzamanlılığı nasıl yönetebilmeniz için kısa bir genel bakış sunulmaktadır."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 676313f8-a158-4e3a-a99b-2c29a341ecc9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: da52a6278a3d3b084dbf5a594db37df8447bb944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a>Hız ve, kodlama eşzamanlılık yönetme

Bu makalede hızı ve kodlama işleri/görevlerinizi eşzamanlılığı nasıl yönetebilmeniz için kısa bir genel bakış sunulmaktadır.

## <a name="overview"></a>Genel Bakış

Media Services, bir **ayrılmış birim türü** ile görevleri işleme medyanızı işlenir hello hızını belirler. Merhaba aşağıdaki arasında seçim yapabilirsiniz ayrılmış birim türleri: **S1**, **S2**, veya **S3**. Örneğin, aynı kodlama işi çalıştıktan daha hızlı hello kullandığınızda hello **S2** ayrılmış birim türü karşılaştırma toohello **S1** türü. Merhaba [kodlama birimleri ölçeklendirme](media-services-scale-media-processing-overview.md) konu arasında farklı kodlama hızları seçerken karar vermenize yardımcı olan bir tablo gösterir.

Ayrıca toospecifying hello ayrılmış birim türü, hesabınızla tooprovision belirtebilirsiniz **ayrılan birimler**. sağlanan ayrılmış birim Hello sayısı belirli bir hesap eşzamanlı olarak işlenebilecek ortam görevleri hello sayısını belirler. Örneğin, beş medya görevler eşzamanlı olarak kadar uzun çalışıyor olacak beş ayrılmış birimler, hesabınız varsa, olarak vardır görevleri toobe işlenir. Merhaba Kalan görevler hello kuyrukta bekler ve sıralı olarak çalışan bir görev tamamlandığında işlemek için toplanmış. Bir hesap sağlanan tüm ayrılan birimler yoksa, ardından görevleri sırayla çekilir. Bu durumda, hello bir görev tamamlama arasındaki süre bekleyin ve hello sonraki bir başlangıç kaynakları hello kullanılabilirliğini hello sistemde bağlıdır.

Ayrıntılı bilgi ve örnekler için nasıl tooscale kodlama birimlerini görmek gösteren [bu](media-services-scale-media-processing-overview.md) konu.

## <a name="next-step"></a>Sonraki adım

[Kodlama ölçek birimleri](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

