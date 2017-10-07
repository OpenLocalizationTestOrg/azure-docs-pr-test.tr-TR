---
title: "aaaHow tooadd bir IOT hub'ı olay kaynağı tooyour Azure zaman serisi Öngörüler ortam | Microsoft Docs"
description: "Bu öğretici bir olay kaynağı başka bir deyişle tooadd tooan IOT hub'ı tooyour zaman serisi Öngörüler ortamı nasıl bağlanacağını kapsar"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: c626f9653d1c012360120fa9fc3d211d7d5beb5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-an-iot-hub-event-source"></a>Nasıl tooadd bir IOT hub'ı olay kaynağı

Bu öğretici nasıl toouse hello Azure portal tooadd bir IOT hub'ı tooyour zaman serisi Öngörüler ortamından okuyan bir olay kaynağı kapsar.

## <a name="prerequisites"></a>Ön koşullar

Bir IOT Hub oluşturdunuz ve olayları tooit yazma. IOT hub'ları hakkında daha fazla bilgi için bkz: <https://azure.microsoft.com/services/iot-hub/>

> [Tüketici grupları] Her zaman serisi Öngörüler olay kaynağı ile herhangi bir tüketiciye paylaşılmayan kendi ayrılmış bir tüketici grubundaki toohave gerekir. Birden çok okuyucular kullanırsa olaylarından Merhaba aynı tüketici grubu, tüm okuyucular büyük olasılıkla toosee hatalarıdır. Merhaba Ayrıntılar için bkz [IOT Hub Geliştirici Kılavuzu](../iot-hub/iot-hub-devguide.md).

## <a name="choose-an-import-option"></a>Bir içe aktarma seçeneği seçin

Merhaba olay kaynağı Hello ayarlarını el ile girilebilir veya IOT hub'ı, kullanılabilir tooyou hello IOT hub'larından seçilebilir.
Merhaba, **alma seçeneği** Seçici, aşağıdaki seçenekleri şu hello birini seçin:

* IOT hub'ı ayarları sağlayın el ile
* Kullanılabilir aboneliklerden IOT hub'ı kullanın

### <a name="select-an-available-iot-hub"></a>Kullanılabilir IOT hub'ı seçin

Merhaba aşağıdaki tabloda her seçenekte açıklamasını hello yeni olay kaynağı sekmesi kullanılabilir IOT hub'ı bir olay kaynağı olarak seçerken açıklanmaktadır:

| ÖZELLİK ADI | AÇIKLAMA |
| --- | --- |
| Olay kaynağı adı | Olay kaynağı Hello adı. Bu ad zaman serisi Öngörüler ortamınızda benzersiz olması gerekir.
| Kaynak | Seçin **IOT hub'ı** toocreate bir IOT hub'ı olay kaynağı.
| Abonelik kimliği | Bu IOT hub'ının oluşturulduğu hello aboneliği seçin.
| IOT hub'ı adı | Merhaba IOT hub'ı Hello adını seçin.
| IOT hub ilke adı | IOT hub'ı Ayarlar sekmesinde hello üzerinde bulunabilir hello paylaşılan erişim ilkesi seçin. Her paylaşılan erişim ilkesinin bir adı, ayarlayın ve erişim anahtarları izinleri vardır. Merhaba paylaşılan erişim ilkesi için olay kaynağı *gerekir* sahip **service bağlanma** izinleri.
| IOT hub tüketici grubu | Merhaba IOT Hub tüketici grubu tooread olaylarından hello. Yüksek oranda olduğu toouse ayrılmış bir tüketici grubu olay kaynağınız için önerilir.

### <a name="provide-iot-hub-settings-manually"></a>IOT hub'ı ayarları sağlayın el ile

Merhaba aşağıdaki tabloda her bir özellik açıklamasını ile Merhaba yeni olay kaynağı sekmesinde ayarları girerken açıklanmaktadır el ile:

| ÖZELLİK ADI | AÇIKLAMA |
| --- | --- |
| Olay kaynağı adı | Olay kaynağı Hello adı. Bu ad zaman serisi Öngörüler ortamınızda benzersiz olması gerekir.
| Kaynak | Seçin **IOT hub'ı** toocreate bir IOT hub'ı olay kaynağı.
| Abonelik kimliği | Bu IOT hub'ının oluşturulduğu hello abonelik.
| Kaynak grubu | Bu IOT hub'ının oluşturulduğu hello abonelik.
| IOT hub'ı adı | IOT Hub'ınızı Hello adı. IOT hub'ınızı oluşturduğunuzda, ona bir özel ad da vermiş
| IOT hub ilke adı | IOT hub'ı Ayarlar sekmesinde hello üzerinde oluşturulabilir hello paylaşılan erişim ilkesi. Her paylaşılan erişim ilkesinin bir adı, ayarlayın ve erişim anahtarları izinleri vardır. Merhaba paylaşılan erişim ilkesi için olay kaynağı *gerekir* sahip **service bağlanma** izinleri.
| IOT hub ilke anahtarı | Merhaba paylaşılan erişim anahtarı tooauthenticate erişim toohello Service Bus ad alanı kullanılır. Merhaba birincil veya ikincil anahtarı buraya girin.
| IOT hub tüketici grubu | Merhaba IOT Hub tüketici grubu tooread olaylarından hello. Yüksek oranda olduğu toouse ayrılmış bir tüketici grubu olay kaynağınız için önerilir.

## <a name="next-steps"></a>Sonraki adımlar

1. Bir veri erişim ilkesi tooyour ortama eklemek [tanımla veri erişim ilkeleri](time-series-insights-data-access.md)
1. Merhaba, ortamınızda erişim [zaman serisi Insights portalı](https://insights.timeseries.azure.com)
