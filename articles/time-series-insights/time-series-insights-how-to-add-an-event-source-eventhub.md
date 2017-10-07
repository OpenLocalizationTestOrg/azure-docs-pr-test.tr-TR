---
title: "bir olay hub'ı olay kaynağı tooyour Azure zaman serisi Öngörüler ortam aaaHow tooadd | Microsoft Docs"
description: "Bu öğretici nasıl tooadd bir olay kaynağı başka bir deyişle bağlı tooan olay hub'ı tooyour zaman serisi Öngörüler ortamı kapsar"
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
ms.openlocfilehash: a98cd91deb51c829084a00c5f2a80b39d0fc511c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-an-event-hub-event-source"></a>Nasıl tooadd bir olay hub'ı olay kaynağı

Bu öğretici nasıl toouse hello Azure portal tooadd bir olay hub'ı tooyour zaman serisi Öngörüler ortamından okuyan bir olay kaynağı kapsar.

## <a name="prerequisites"></a>Ön koşullar

Bir Event Hub oluşturdunuz ve olayları tooit yazma. Event Hubs hakkında daha fazla bilgi için bkz: <https://azure.microsoft.com/services/event-hubs/>

> [Tüketici grupları] Her zaman serisi Öngörüler olay kaynağı ile herhangi bir tüketiciye paylaşılmayan kendi ayrılmış bir tüketici grubundaki toohave gerekir. Birden çok okuyucular kullanırsa olaylarından Merhaba aynı tüketici grubu, tüm okuyucular büyük olasılıkla toosee hatalarıdır. Ayrıca olay hub'ı başına 20 tüketici grupları sınırı yoktur. Merhaba Ayrıntılar için bkz [Event Hubs Programlama Kılavuzu](../event-hubs/event-hubs-programming-guide.md).

## <a name="choose-an-import-option"></a>Bir içe aktarma seçeneği seçin

Merhaba olay kaynağı Hello ayarlarını el ile girilebilir veya bir olay hub'ı, kullanılabilir tooyou hello olay hub'larından seçilebilir.
Merhaba, **alma seçeneği** Seçici, aşağıdaki seçenekleri şu hello birini seçin:

* Olay hub'ı ayarları sağlayın el ile
* Kullanılabilir aboneliklerden olay hub'ı kullanın

### <a name="select-an-available-event-hub"></a>Kullanılabilir bir olay hub'ı seçin

Merhaba aşağıdaki tabloda her seçenek hello yeni olay kaynağı sekmesinde açıklamasını ile bir olay kaynağı olarak kullanılabilir bir Event Hub seçerken açıklanmaktadır:

| ÖZELLİK ADI | AÇIKLAMA |
| --- | --- |
| Olay kaynağı adı | Olay kaynağı Hello adı. Bu ad zaman serisi Öngörüler ortamınızda benzersiz olması gerekir.
| Kaynak | Seçin **olay hub'ı** toocreate bir olay hub'ı olay kaynağı.
| Abonelik kimliği | Bu olay hub'ının oluşturulduğu hello aboneliği seçin.
| Hizmet veri yolu ad alanı | Merhaba olay hub'ı içeren hello hizmet veri yolu ad alanını seçin.
| Olay hub'ı adı | Merhaba adını hello olay hub'ı seçin.
| Olay hub'ı ilke adı | Merhaba olay hub'ı yapılandırma sekmesinde oluşturulan hello paylaşılan erişim ilkesi seçin. Her paylaşılan erişim ilkesinin bir adı, ayarlayın ve erişim anahtarları izinleri vardır. Merhaba paylaşılan erişim ilkesi için olay kaynağı *gerekir* sahip **okuma** izinleri.
| Olay hub tüketici grubu | Merhaba tüketici grubu tooread olayları hello olay hub'ı. Yüksek oranda olduğu toouse ayrılmış bir tüketici grubu olay kaynağınız için önerilir.

### <a name="provide-event-hub-settings-manually"></a>Olay hub'ı ayarları sağlayın el ile

Merhaba aşağıdaki tabloda her bir özellik açıklamasını ile Merhaba yeni olay kaynağı sekmesinde ayarları girerken açıklanmaktadır el ile:

| ÖZELLİK ADI | AÇIKLAMA |
| --- | --- |
| Olay kaynağı adı | Olay kaynağı Hello adı. Bu ad zaman serisi Öngörüler ortamınızda benzersiz olması gerekir.
| Kaynak | Seçin **olay hub'ı** toocreate bir olay hub'ı olay kaynağı.
| Abonelik kimliği | Bu olay hub'ının oluşturulduğu hello abonelik.
| Kaynak grubu | Bu olay hub'ının oluşturulduğu hello abonelik.
| Hizmet veri yolu ad alanı | Bir hizmet veri yolu ad alanı, Mesajlaşma varlıkları kümesine ilişkin bir kapsayıcıdır. Yeni bir olay hub'ı oluşturduğunuzda, hizmet veri yolu ad alanı da oluşturmuş olursunuz.
| Olay hub'ı adı | Olay Hub'ınızı Hello adı. Olay hub'ınızı oluşturduğunuzda, ona bir özel ad da vermiş
| Olay hub'ı ilke adı | Merhaba olay hub'ı yapılandırma sekmesinde oluşturulan hello paylaşılan erişim ilkesi. Her paylaşılan erişim ilkesinin bir adı, ayarlayın ve erişim anahtarları izinleri vardır. Merhaba paylaşılan erişim ilkesi için olay kaynağı *gerekir* sahip **okuma** izinleri.
| Olay hub'ı İlkesi anahtarı | Merhaba paylaşılan erişim anahtarı tooauthenticate erişim toohello Service Bus ad alanı kullanılır. Merhaba birincil veya ikincil anahtarı buraya girin.
| Olay hub tüketici grubu | Merhaba tüketici grubu tooread olayları hello olay hub'ı. Yüksek oranda olduğu toouse ayrılmış bir tüketici grubu olay kaynağınız için önerilir.

## <a name="next-steps"></a>Sonraki adımlar

1. Bir veri erişim ilkesi tooyour ortama eklemek [tanımla veri erişim ilkeleri](time-series-insights-data-access.md)
1. Merhaba, ortamınızda erişim [zaman serisi Insights portalı](https://insights.timeseries.azure.com)
