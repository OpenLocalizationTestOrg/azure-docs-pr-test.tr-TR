---
title: "aaaIntroduction tooStream Analytics penceresi işlevleri | Microsoft Docs"
description: "Akış (dönen atlamalı, kayan) analizi hello üç pencere işlevleri hakkında bilgi edinin."
keywords: "dönen pencere, kayan pencere atlamalı pencere"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0d8d8717-5d23-43f0-b475-af078ab4627d
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 7fc36eb9afb2b28e2791d925d26923145eb38074
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toostream-analytics-window-functions"></a>Giriş tooStream Analytics penceresi işlevleri
Pek çok gerçek senaryoları akış, onu yalnızca zamana bağlı Windows'da bulunan hello verileri üzerinde gerekli tooperform işlemler saattir. Pencereleme işlevler için yerel destek karmaşık akış işleme işleri yazma, geliştirici üretkenliğine hello iğnenin taşır Azure akış analizi, anahtar bir özelliğidir. Akış analizi sağlar geliştiriciler toouse [ **dönen**](https://msdn.microsoft.com/library/dn835055.aspx), [ **Hopping** ](https://msdn.microsoft.com/library/dn835041.aspx) ve [ **hareketli** ](https://msdn.microsoft.com/library/dn835051.aspx) windows tooperform zamana bağlı işlemleri veri akışı üzerinde. Değer belirtmeye olan tüm [penceresi](https://msdn.microsoft.com/library/dn835019.aspx) operations çıktı hello sonuçlarına **son** hello penceresinin. Merhaba penceresinde Hello çıktısını tek olay kullanılan hello üzerinde toplama işlevi tabanlı olacaktır. Merhaba olay hello zaman damgası hello penceresinde hello ucunun sahip olur ve tüm pencere işlevleri sabit uzunluk ile tanımlanır. Son olarak tüm pencere işlevleri kullanılmalıdır önemli toonote olan bir [ **GROUP BY** ](https://msdn.microsoft.com/library/dn835023.aspx) yan tümcesi.

![Stream Analytics penceresi işlevleri kavramları](media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a>Atlayan pencere
Dönen pencere işlevleri kullanılan toosegment ayrı zaman parçalara veri akışı olan ve bunları karşı işlevi Merhaba örneği aşağıdaki gibi gerçekleştirin. Merhaba anahtar differentiators atlayan pencere, bunlar yinelemeniz, çakışmaması ve bir olay bir atlayan pencere daha toomore ait olamaz ' dir.

![Giriş dönen stream Analytics penceresi işlevleri](media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a>Atlamalı pencere
Atlamalı pencere işlevleri atlama İleri zamanına göre sabit bir süre içinde. Olayları bir Hopping penceresi sonuç kümesi'den toomore ait olabilir. böylece bunların kolay toothink binebilir, dönen windows olarak olabilir. toomake Hopping penceresinde hello aynı biri yalnızca belirtirsiniz atlayan pencere hello atlama boyutu toobe hello aynı hello pencere boyutu. 

![Stream Analytics penceresi atlamalı giriş işlevleri](media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a>Kayan pencere
Dönen veya atlamalı windows, farklı olarak, kayan pencere işlevleri bir çıktı üretir **yalnızca** olay oluştuğunda. Her penceresinde en az bir olay sahip olur ve hello penceresi sürekli bir € (epsilon) ileri taşır. Atlamalı Windows gibi olayların bir kayan pencere daha toomore ait olabilir.

![Stream Analytics penceresi kayan giriş işlevleri](media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a>Pencere işlevleri ile ilgili Yardım alma
Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.

## <a name="next-steps"></a>Sonraki adımlar
* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)

