---
title: "Ayrıca Azure akış analizi veri güdümlü hello iş diyagramı kullanarak hata ayıklama | Microsoft Docs"
description: "Stream Analytics işiniz hello iş diyagramı ve ölçümleri kullanarak sorun giderin."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/01/2017
ms.author: jeffstok
ms.openlocfilehash: 1af884d485bebb06b034da01a13f7f8240516571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-driven-debugging-by-using-hello-job-diagram"></a>Veri temelli hello iş diyagramı kullanarak hata ayıklama

Merhaba iş hello diyagramda **izleme** dikey penceresinde hello Azure portal iş hattınızı görselleştirmenize yardımcı olabilir. Giriş, çıkış ve sorgu adımları gösterir. Toomore sorunları giderirken bir sorunun hello kaynağını hızlı bir şekilde ayırmak, her adımı için hello iş diyagramı tooexamine hello ölçümleri kullanabilirsiniz.

## <a name="using-hello-job-diagram"></a>Merhaba iş diyagramı kullanma

Hello Azure portal'ın altında bir Stream Analytics işinde while **destek + sorun giderme**seçin **iş diyagramı**:

![Ölçümleri - konumu ile iş diyagramı](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

Her sorgu adım toosee hello karşılık gelen bölüm bölmesinde düzenleme sorguda seçin. Merhaba adım için bir ölçüm grafik hello sayfasında alt bölmesinde görüntülenir.

![Ölçümleri - temel iş ile iş diyagramı](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

hello Azure Event Hubs'a giriş toosee hello bölümleri seçin **...** Bir bağlam menüsü görüntülenir. Merhaba giriş birleşme de görebilirsiniz.

![Diyagram ölçümlerle iş - bölümü genişletin](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

yalnızca tek bir bölüm, select hello bölümü düğümü için toosee hello ölçüm grafik. Merhaba ölçümleri hello sayfasının hello altında gösterilir.

![Ölçümleri - daha fazla ölçümleri ile iş diyagramı](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

bir birleşme select hello birleşme düğümü için toosee hello ölçümleri grafik. Grafik aşağıdaki hello hiçbir olay bırakılan veya ayarlanmış gösterir.

![İş diyagramı - ölçümlerle kılavuz](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

Merhaba ölçüm değer ve zaman noktası toohello grafik toosee hello ayrıntıları.

![Diyagram ölçümlerle iş - getirin](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a>Ölçümleri kullanarak sorun giderme

Merhaba **QueryLastProcessedTime** ölçüm, belirli bir adıma veri alındığında gösterir. Merhaba topoloji bakarak hello çıkış işlemci toosee hangi adımın veri almıyor geriye doğru çalışabilir. Bir adımı veri alamıyorsanız, toohello sorgu adımı hemen önce gidin. Merhaba önceki sorgu adımı bir zaman penceresi olup olmadığını ve bunun için yeterli süre geçtiyse denetleyin toooutput veri. (Windows açıldı toohello saat olan Not bundan.)
 
Merhaba önceki sorgu adımı bir giriş işlemci ise, hedeflenen sorular aşağıdaki hello giriş ölçümleri toohelp yanıt hello kullanın. Bunlar, bir iş giriş kaynaklardan veri alma olup olmadığını belirlemenize yardımcı olabilir. Merhaba sorgu bölümlenmiş varsa her bölüm inceleyin.
 
### <a name="how-much-data-is-being-read"></a>Ne kadar veri okunan?

*   **InputEventsSourcesTotal** okuma veri birimleri hello sayısıdır. Örneğin, BLOB sayısı hello.
*   **InputEventsTotal** okuma olay hello sayısıdır. Bu ölçüm her bölüm için kullanılabilir.
*   **InputEventsInBytesTotal** hello okunan bayt sayısı.
*   **InputEventsLastArrivalTime** alınan her olayın sıraya alınan saatiyle güncelleştirilir.
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a>Zaman ilerleyen? Gerçek olayları okuyorsanız noktalama verilen değil.

*   **InputEventsLastPunctuationTime** tookeep zaman taşıma bir noktalama zaman verilmiş gösterir ilet. Noktalama işaretleri verilmemiş, veri akışı engellenen.
 
### <a name="are-there-any-errors-in-hello-input"></a>Merhaba girişinde hataları var mı?

*   **InputEventsEventDataNullTotal** null veri olayları sayısıdır.
*   **InputEventsSerializerErrorsTotal** doğru serisi kaldırılamadı olayların sayısıdır.
*   **InputEventsDegradedTotal** seri durumdan çıkarma dışında bir sorunla olayların sayısıdır.
 
### <a name="are-events-being-dropped-or-adjusted"></a>Olayları bırakılan veya ayarlanmış misiniz?

*   **InputEventsEarlyTotal** hello yüksek Filigran önce bir uygulama zaman damgası olan olayları hello sayısıdır.
*   **InputEventsLateTotal** hello yüksek Filigran sonra bir uygulama zaman damgası olan olayları hello sayısıdır.
*   **InputEventsDroppedBeforeApplicationStartTimeTotal** hello sayı olayı hello iş başlangıç saatinden önce bırakıldı.
 
### <a name="are-we-falling-behind-in-reading-data"></a>Biz veri okuma dönmeden?

*   **InputEventsSourcesBackloggedTotal** toobe kaç tane daha fazla ileti gereksinim söyler olay hub'ları ve Azure IOT Hub girdileri okuyun.


## <a name="get-help"></a>Yardım alın
Ek Yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Sonraki adımlar
* [Giriş tooStream analizi](stream-analytics-introduction.md)
* [Stream Analytics ile çalışmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Stream Analytics işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Stream Analytics sorgu dili başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Stream Analytics Yönetimi REST API Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)
