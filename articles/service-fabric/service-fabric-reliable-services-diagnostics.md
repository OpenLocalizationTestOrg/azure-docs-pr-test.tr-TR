---
title: "aaaStateful Reliable Services tanılama | Microsoft Docs"
description: "Durum Bilgisi Olan Reliable Services için tanılama işlevi"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ae0e8f99-69ab-4d45-896d-1fa80ed45659
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 6200800b858957c06039d9af062633b12a446318
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostic-functionality-for-stateful-reliable-services"></a>Durum Bilgisi Olan Reliable Services için tanılama işlevi
Merhaba durum bilgisi olan güvenilir hizmetler StatefulServiceBase sınıfı yayar [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) kullanılan toodebug olabilen olaylar Merhaba hizmeti, içine nasıl hello çalışma zamanı işletim ve sorunu gidermenize yardımcı bilgiler.

## <a name="eventsource-events"></a>EventSource olaylarını
Merhaba EventSource hello durum bilgisi olan güvenilir hizmetler StatefulServiceBase sınıfı için "Microsoft ServiceFabric Hizmetleri" adıdır. Bu olay kaynağı olaylarından görünür [tanılama olayları](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md#view-service-fabric-system-events-in-visual-studio) hello hizmeti yüklenirken pencere [Visual Studio'da hata ayıklaması](service-fabric-debugging-your-application.md).

Araçlar ve toplama ve/veya EventSource olaylarını görüntüleme içinde yardımcı teknolojiler örnekleri [PerfView](http://www.microsoft.com/download/details.aspx?id=28567), [Microsoft Azure tanılama](../cloud-services/cloud-services-dotnet-diagnostics.md)ve [Microsoft TraceEvent Library](http://www.nuget.org/packages/Microsoft.Diagnostics.Tracing.TraceEvent).

## <a name="events"></a>Olaylar
| Olay adı | Olay Kimliği | Düzey | Olay açıklaması |
| --- | --- | --- | --- |
| StatefulRunAsyncInvocation |1 |Bilgilendirme |Hizmet RunAsync görevi başlatıldığında yayılan |
| StatefulRunAsyncCancellation |2 |Bilgilendirme |Hizmet RunAsync görevi iptal edildiğinde yayılan |
| StatefulRunAsyncCompletion |3 |Bilgilendirme |Hizmet RunAsync görev tamamlandığında yayılan |
| StatefulRunAsyncSlowCancellation |4 |Uyarı |Hizmet RunAsync görevi uzun toocomplete iptal yönlendirdiğinde yayılan |
| StatefulRunAsyncFailure |5 |Hata |Hizmet RunAsync görev özel durum oluşturduğunda yayılan |

## <a name="interpret-events"></a>Olayları yorumlama
StatefulRunAsyncInvocation, StatefulRunAsyncCompletion ve StatefulRunAsyncCancellation olaylardır, yararlı toohello hizmet yazan toounderstand hello ömrü, hizmet zaman başlatıldı, iptal edildi veya tamamlandı hello zamanlama yanı sıra bir hizmet-- . Bu hizmet sorunları veya anlama hello hizmet yaşam döngüsü ayıklarken yararlı olabilir.

Merhaba hizmetiyle ilgili sorunlara belirttiğinden hizmeti yazıcıları Kapat dikkat tooStatefulRunAsyncSlowCancellation ve StatefulRunAsyncFailure olayları ödeme.

Merhaba hizmet RunAsync() görevi aykırı her StatefulRunAsyncFailure yayınlanır. Genellikle, oluşturulan bir özel bir hata veya hello hizmetinde hata gösterir. Ayrıca, taşınan tooa farklı bir düğüme olacak şekilde hello özel durum hello hizmet toofail neden olur. Bu, pahalı bir işlem olabilir ve hello hizmet taşınırken gelen istekleri geciktirebilir. Beklemeleri hello özel durum hello nedenini ve mümkünse, bunu azaltmak.

İptal isteği hello RunAsync görev için dört saniyeden daha uzun sürer her StatefulRunAsyncSlowCancellation yayınlanır. Bir hizmeti uzun toocomplete iptal aldığında, hızlı bir şekilde başka bir düğümde yeniden hello hizmet toobe hello yeteneği etkiler. Bu etkileyebilir hello hello hizmetinin genel kullanılabilirlik.

## <a name="next-steps"></a>Sonraki adımlar
* [PerfView EventSource sağlayıcıları](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
