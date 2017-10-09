---
title: "Olay hub'ı alıcıları ile aaaDebug Azure akış analizi | Microsoft Docs"
description: "Olay hub'ları tüketici grupları, Stream Analytics işlerini dikkate için en iyi uygulamaları sorgulayın."
keywords: "Olay hub'ı sınırı, tüketici grubu"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 89821e6273151de43b5e42d907e547c939e24824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a>Azure Stream Analytics olay hub'ı alıcıları ile hata ayıklama

Azure Event Hubs Azure akış analizi tooingest çıktı verileri veya bir iş kullanabilirsiniz. Olay hub'ları kullanmak için en iyi uygulama toouse olan birden çok tüketici grupları, tooensure iş ölçeklenebilirlik. Belirli bir giriş için hello Stream Analytics işinde okuyucu hello sayısını hello tek bir tüketici grubundaki okuyucu sayısını etkiler bir nedenidir. Merhaba kesin alıcıları sayısı iç uygulama ayrıntılarını hello genişleme topoloji mantığı için temel alır. Alıcıları Hello sayısı harici olarak gösterilmez. Okuyucu Hello sayısını hello iş başlangıç saatinde veya iş yükseltme sırasında değiştirebilirsiniz.

> [!NOTE]
> Okuyucu Hello sayısını iş yükseltme sırasında değiştiğinde geçici uyarıları tooaudit günlüklerine yazılır. Akış analizi işleri, bu geçici sorunları otomatik olarak kurtarın.

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a>Bölüm başına okuyucu sayısını beş olay hub'ları sınırını aşıyor

Hangi hello bölüm başına okuyucu sayısını beş hello olay hub'ları sınırını aşıyor. senaryoları hello şunları içerir:

* Birden çok SELECT deyimine: çok başvuran birden çok SELECT deyimine kullanırsanız**aynı** olay hub'ı girin, her SELECT deyiminin oluşturulan yeni bir alıcı toobe neden olur.
* BİRLEŞİM: bir birleşim kullandığınızda, olası toohave olmasından toohello başvuran birden çok girişi **aynı** olay hub'ı ve tüketici grubu.
* Kendi KENDİNE BİRLEŞİMDE: SELF katılma işlemi kullandığınızda, olası toorefer toohello olmasından **aynı** olay hub'ı birden çok kez.

## <a name="solution"></a>Çözüm

Merhaba aşağıdaki en iyi yöntemleri hangi hello bölüm başına okuyucu sayısını beş hello olay hub'ları sınırını aşıyor. senaryoları azaltılmasına yardımcı olur.

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a>WITH yan tümcesini kullanarak sorgunuzu içine birden çok adımı bölme

Merhaba WITH yan tümcesi hello sorgusunda FROM yan tümcesi tarafından başvurulan bir geçici adlandırılmış sonuç kümesi belirtir. Merhaba WITH yan tümcesi hello yürütme kapsamında tek bir SELECT deyimi tanımlayın.

Örneğin, bu sorgu yerine:

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

Bu sorguyu kullanın:

```
WITH input (
   SELECT * FROM inputEventHub
) as data

SELECT foo
INTO output1
FROM data

SELECT bar
INTO output2
FROM data
…
```

### <a name="ensure-that-inputs-bind-toodifferent-consumer-groups"></a>Girişleri toodifferent tüketici grupları bağlamak emin olun

Üç veya daha fazla girdi bağlı toohello olan sorguları için aynı olay hub'ları tüketici grubunda, ayrı tüketici grupları oluşturun. Bu ek Stream Analytics girişleri hello oluşturulmasını gerektirir.


## <a name="get-help"></a>Yardım alın
Ek Yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Sonraki adımlar
* [Giriş tooStream analizi](stream-analytics-introduction.md)
* [Stream Analytics ile çalışmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Stream Analytics işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Stream Analytics sorgu dili başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Stream Analytics Yönetimi REST API Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)
