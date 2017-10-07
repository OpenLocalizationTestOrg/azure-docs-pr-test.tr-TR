---
title: "Azure Application Insights algılama aaaSmart | Microsoft Docs"
description: "Application Insights uygulama telemetrinin otomatik derin çözümleme yapar ve olası sorunları sizi uyarır."
services: application-insights
documentationcenter: windows
author: rakefetj
manager: carmonm
ms.assetid: 2eeb4a35-c7a1-49f7-9b68-4f4b860938b2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: f794476088fc69154eda2077b7a5cdc769fab3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection-in-application-insights"></a>Application ınsights'ta akıllı algılama
 Akıllı algılama, web uygulamanızın olası performans sorunları otomatik olarak sizi uyarır. Uygulamanız çok gönderir hello telemetri öngörülü çözümlemesi gerçekleştirir[Application Insights](app-insights-overview.md). Başarısızlık oranları ani bir artışa veya istemci veya sunucu performans anormal desenlerini ise bir uyarı alırsınız. Bu özellik, herhangi bir yapılandırma gerekir. Uygulamanız yeterli telemetri gönderirse çalışır.

Akıllı algılama uyarıları hem aldığınız hello e-postalar ve hello akıllı algılama dikey penceresinden erişebilirsiniz.

## <a name="review-your-smart-detections"></a>Akıllı algılamaların gözden geçirin
İki yolla algılamaların bulabilir:

* **Bir e-posta aldığınız** Application Insights gelen. Aşağıda, genel bir örnek verilmiştir:
  
    ![E-posta uyarısı](./media/app-insights-proactive-diagnostics/03.png)
  
    Merhaba büyük düğme tooopen daha ayrıntılı olarak hello portal'ı tıklatın.
* **Merhaba akıllı algılama döşeme** uygulamanızın bir genel bakış dikey son uyarıların sayısını gösterir. Merhaba döşeme toosee son uyarıların bir listesi'ı tıklatın.

![Görünümü en son algılama](./media/app-insights-proactive-diagnostics/04.png)

Bir uyarı toosee ayrıntılarını seçin.

## <a name="what-problems-are-detected"></a>Hangi sorunlar algılandığında?
Algılama üç tür vardır:

* [Algılama - hatası anormallikleri akıllı](app-insights-proactive-failure-diagnostics.md). Machine learning kullanırız yük ve diğer etkenlere bağlı ile ilişkilendirerek, uygulamanız için başarısız isteklerin tooset beklenen hello oranı. Merhaba hata oranı hello beklenen zarfının dışında kalırsa, size bir uyarı göndereceğiz.
* [Algılama - performans Anormalliklerini akıllı](app-insights-proactive-performance-diagnostics.md). Yanıt süresi bir işlem veya bağımlılık sürenin karşılaştırılan toohistorical temel yavaşlamasını veya yanıt süresi veya sayfa yükleme süresi anormal bir desen tanımlamak bildirimler alın.   
* [Akıllı algılama - Azure bulut hizmeti sorunları](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/). Uygulamanızı Azure bulut Hizmetleri'nde barındırılan ve rol örneği başlatma hataları, sık sık geri dönüştürülüyor veya çalışma zamanı çökme (Crash) varsa, uyarılar alırsınız.

(her bir bildirim hello Yardım bağlantıları toohello ilgili makaleler atmanız.)

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Sonraki adımlar
Bu tanılama araçları hello telemetriyi uygulamanızdan incelemek yardımcı olur:

* [Ölçüm Gezgini](app-insights-metrics-explorer.md)
* [Arama Gezgini](app-insights-diagnostic-search.md)
* [Analizi - güçlü sorgu dili](app-insights-analytics-tour.md)

Akıllı algılama tamamen otomatik olarak yapılır. Ancak, belki de daha fazla bazı uyarılar tooset ister misiniz?

* [El ile yapılandırılmış ölçüm uyarıları](app-insights-alerts.md)
* [Kullanılabilirlik web testleri](app-insights-monitor-web-app-availability.md) 

