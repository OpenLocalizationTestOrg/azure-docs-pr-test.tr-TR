---
title: "aaaAdd başvuru veri kümesi tooyour Azure zaman serisi Öngörüler ortamı | Microsoft Docs"
description: "Bu öğreticide, başvuru veri kümesi tooyour zaman serisi Öngörüler ortam Ekle"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: venkatja
ms.openlocfilehash: 05e626ed81a22f2a8710b23a931ccd17c0f38ca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-reference-data-set-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a>Merhaba Ibiza portalını kullanarak, zaman serisi Öngörüler ortamınız için bir başvuru veri kümesi oluşturma

Bir başvuru veri kümesi, olay kaynağınızdan hello olaylarla engagement'ta öğeleri koleksiyonudur. Zaman Serisi Görüşleri giriş altyapısı, olay kaynağınızdaki bir olay ile başvuru veri kümenizdeki bir öğeyi birleştirir. Bu genişletilmiş olay daha sonra sorgu için kullanılabilir. Bu katılımı hello tuşları başvuru veri kümesinde tanımlanan temel alır.

## <a name="steps-tooadd-a-reference-data-set-tooyour-environment"></a>Adımları tooadd bir başvuru veri kümesi tooyour ortamı

1. İçinde toohello oturum [Ibiza portalını](https://portal.azure.com).
2. "Tüm kaynaklar" Merhaba Ibiza portalında sol tarafındaki hello hello menüsünde'ı tıklatın.
3. Zaman Serisi Görüşleri ortamınızı seçin.

    ![Merhaba zaman serisi Öngörüler başvuru veri kümesi oluşturma](media/add-reference-data-set/getstarted-create-reference-data-set-1.png)

4. "Başvuru Veri Kümeleri" seçeneğini belirleyin ve "+ Ekle" öğesine tıklayın.

    ![Merhaba zaman serisi Öngörüler başvuru veri kümesi - Ayrıntılar oluşturma](media/add-reference-data-set/getstarted-create-reference-data-set-2.png)

5. Merhaba hello başvuru veri kümesinin adını belirtin.
6. Merhaba anahtar adını ve türünü belirtin. Bu ada ve türe özelliğidir kullanılan toopick hello doğru olay kaynağınızda hello olaydan. Örneğin, "DeviceId" anahtar adı ve türü "Dize" olarak sağlarsanız, ardından zaman serisi türü "Dize" Merhaba gelen olay "DeviceID" Merhaba adında bir özellik giriş altyapısı arar Öngörüler hello. Birden fazla anahtar toojoin hello olayla sağlayabilir. Merhaba özellik adı eşleşir büyük/küçük harf duyarlıdır.

     ![Merhaba zaman serisi Öngörüler başvuru veri kümesi - Ayrıntılar oluşturma](media/add-reference-data-set/getstarted-create-reference-data-set-3.png)

7. “Oluştur” düğmesine tıklayın.

## <a name="next-steps"></a>Sonraki adımlar

* [Başvuru verilerini programlamayla yönetin](time-series-insights-manage-reference-data-csharp.md).
* Merhaba tam API başvuru için bkz: [başvuru veri API](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) belge.
