---
title: "bir olay kaynağı tooyour Azure zaman serisi Öngörüler ortam aaaAdd | Microsoft Docs"
description: "Bu öğreticide, bir olay kaynağı tooyour zaman serisi Öngörüler ortama bağlanma"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: omravi
ms.openlocfilehash: 817df5e81cb4dc3d7376914a4651aabebadbcc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a>Merhaba Ibiza portalını kullanarak, zaman serisi Öngörüler ortamınız için bir olay kaynağı oluşturma

Zaman Serisi Görüşleri Olay Kaynağı, Azure Event Hubs gibi bir olay aracısından türetilir. Zaman serisi Öngörüler tooEvent kaynakları, kullanıcıların toowrite tek satırlık bir kod gerek kalmadan hello veri akışı alma doğrudan bağlanır. Şu anda Zaman Serisi Görüşleri, Azure Event Hubs'ı ve Azure IoT Hub'larını destekler. Hello gelecekteki, daha fazla olay kaynakları eklenir.

## <a name="steps-tooadd-an-event-source-tooyour-environment"></a>Adımları tooadd bir olay kaynağı tooyour ortamı

1.  İçinde toohello oturum [Ibiza portalını](https://portal.azure.com).
2.  "Tüm kaynaklar" Merhaba Ibiza portalında sol tarafındaki hello hello menüsünde'ı tıklatın.
3.  Zaman Serisi Görüşleri ortamınızı seçin.

  ![Merhaba zaman serisi Öngörüler olay kaynağı oluşturma](media/add-event-source/getstarted-create-event-source-1.png)

4.  “Olay Kaynakları” öğesini seçin ve “+ Ekle” düğmesine tıklayın.

  ![Merhaba zaman serisi Öngörüler olay kaynağı - Ayrıntılar](media/add-event-source/getstarted-create-event-source-2.png)

5.  Merhaba hello olay kaynağı adını belirtin. Bu ad, bu olay kaynağından gelen tüm olaylarla ilişkilendirilmiştir ve sorgu zamanında kullanılabilir.
6.  Olay hub'ı kaynakların hello geçerli abonelikte hello listeden bir olay hub'ı seçin. Aksi takdirde içeri aktarma seçeneği "sağla olay hub'ı ayarlarını el ile" toospecify bir event hub'ında başka bir abonelik. Olayların JSON biçiminde yayımlanması gerekir.
7.  Okuma izni hello event hub'ındaki ilkesini seçin.
8.  Olay hub’ı tüketici grubunu seçin.

  > [!IMPORTANT]
  > Bu tüketici grubunun başka hiçbir hizmet (örneğin, Stream Analytics işi veya başka bir Zaman Serisi Görüşleri ortamı) tarafından kullanılmadığından emin olun. Bir tüketici grubundaki diğer hizmetler tarafından kullanılıyorsa, işlem olumsuz bu ortam için etkilenen okuyun ve diğer hizmetleri hello. "$Default" Merhaba tüketici grubu olarak kullanıyorsanız, diğer okuyucular tarafından toopotential yeniden yol açabilir.

9.  “Oluştur” düğmesine tıklayın.

Merhaba olay kaynağı oluşturulduktan sonra zaman serisi Öngörüler ortamınıza veri akış otomatik olarak başlatılacak.

## <a name="next-steps"></a>Sonraki adımlar

* [Olayları göndermek](time-series-insights-send-events.md) toohello olay kaynağı
* [Zaman Serisi Görüşleri Portalı](https://insights.timeseries.azure.com)’nda ortamınızı görüntüleme
