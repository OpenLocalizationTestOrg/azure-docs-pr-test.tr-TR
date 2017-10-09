---
title: "aaaUnderstanding Stream Analytics işi izleme | Microsoft Docs"
description: "Akış analizi işi izleme anlama"
keywords: Sorgu izlemesi
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5f5cc00f-4a7b-491e-89e1-dbafea46d399
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 36819025c7b2ddbf4b9694522f1b4820407ca5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-toomonitor-queries"></a>Akış analizi işi izleme anlamak ve nasıl toomonitor sorguları

## <a name="introduction-hello-monitor-page"></a>Giriş: hello izleme sayfası
Merhaba kullanılan toomonitor ve sorgu ve iş performans sorunlarını giderme temel performans ölçümlerini yüzey hem de Azure portal. toosee bu ölçümleri gözatmak için ölçümleri ve görünüm hello görmeniz ilginizi toohello Stream Analytics işi **izleme** hello genel bakış sayfasında bölüm.  

![Bağlantı izleme](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

Merhaba penceresinde gösterildiği gibi görünür:

![İzleme işi Panosu](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a>Akış analizi için kullanılabilir ölçümleri
| Ölçüm                 | Tanım                               |
| ---------------------- | ---------------------------------------- |
| SU % kullanımı       | Merhaba Hello kullanımı akış birimi hello ölçek sekmesinden hello işin tooa iş atanır. Bu gösterge % 80 ulaşmalıdır ya da yukarıdaki mevcut olay işleme gecikebilir veya ilerleme durduruldu yüksek olasılık. |
| Giriş olayları           | Olayların sayısını de hello Stream Analytics işinde tarafından alınan veri miktarı. Bu olaylar toohello giriş kaynağı gönderilme kullanılan toovalidate olabilir. |
| Çıkış olayları          | Merhaba Stream Analytics işi toohello çıkış hedef olayların sayısı tarafından gönderilen veri miktarı. |
| Düzen dışı olayları    | Bırakılan veya olay sıralama İlkesi hello üzerinde temel ayarlanmış bir zaman damgası, verilen sıra dışında alınan olayların sayısı. Bu hello sırası tolerans penceresi ayarı hello yapılandırması tarafından etkilenebilir. |
| Veri dönüştürme hataları | Akış analizi işi tarafından oluşturulan veri dönüştürme hatası sayısı. |
| Çalışma zamanı hataları         | Akış analizi işi yürütme sırasında gerçekleşecek hatalarının toplam sayısını Hello. |
| Geç giriş olayları      | Merhaba olay sıralama İlkesi yapılandırmasına göre hello geç gerçekleşme tolerans penceresi ayarı ya da bırakılan hello kaynak ya da kendi zaman damgası geç gelen olayların sayısının ayarlandı. |
| İşlev istekleri      | Çağrıları toohello Azure Machine Learning işlevi (varsa) sayısı. |
| Başarısız işleve istekleri | Başarısız Azure Machine Learning işlev çağrıları (varsa) sayısı. |
| İşlev olayları        | Olay sayısı, (varsa) toohello Azure Machine Learning işlevi gönderdi. |
| Giriş olayı bayt      | Bayt cinsinden hello akış analizi işi tarafından alınan veri miktarı. Bu olaylar toohello giriş kaynağı gönderilme kullanılan toovalidate olabilir. |


## <a name="customizing-monitoring-in-hello-azure-portal"></a>İzleme hello Azure portalını özelleştirme
Grafik, gösterilen ölçümleri hello türünü ayarlayın ve hello grafiği Düzenle ayarları aralığında saat. Ayrıntılar için bkz [nasıl tooCustomize izleme](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).

  ![Sorgu izleme saati grafiği](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a>Yardım alın
Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.

## <a name="next-steps"></a>Sonraki adımlar
* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)

