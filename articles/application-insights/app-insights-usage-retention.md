---
title: "Azure Application Insights ile web uygulamaları için aaaUser bekletme analizi | Microsoft docs"
description: "Kaç kullanıcının tooyour uygulamaya dönün?"
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: 8bcee5f1611afbd69016ec3eef27832c304762a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a>Application Insights ile web uygulamaları için kullanıcı bekletme çözümlemesi

Merhaba bekletme özelliği [Azure Application Insights](app-insights-overview.md) kaç kullanıcı analiz yardımcı dönmek tooyour uygulama ve ne sıklıkta belirli görevleri veya hedeflerinize ulaşmak. Örneğin, bir oyun sitesi çalıştırırsanız, kimin kazanan sonra iade toohello site hello numarasıyla oyun kaybettikten sonra iade kullanıcıların hello sayıları karşılaştırma. Bu bilgi, kullanıcı deneyiminizi ve iş stratejinizi geliştirmenize yardımcı olabilir.

## <a name="get-started"></a>başlarken

Merhaba Application Insights portalında hello bekletme aracında veri henüz görmüyorsanız, [tooget hello kullanım araçları ile çalışmaya nasıl bilgi](app-insights-usage-overview.md).

## <a name="hello-retention-tool"></a>Merhaba bekletme aracı

![Elde tutma aracı](./media/app-insights-usage-retention/retention.png)

1. Hello araç toocreate yeni bekletme Raporlar kullanıcılara, varolan bekletme raporları açın, geçerli bekletme raporu kaydedin veya farklı kaydet, yapılan değişiklikleri toosaved raporları geri, hello raporu, e-posta veya doğrudan bağlantı ve erişim hello aracılığıyla paylaşımı rapor verileri Yenile belgeler sayfası. 
2. Varsayılan olarak, bekletme herhangi bir şey mi tüm kullanıcılar daha sonra geri geldiği ve belirli bir süre boyunca başka bir şey mi gösterir. Olayları toonarrow hello belirli kullanıcı etkinlikleri odaklanmak farklı bileşimini seçebilirsiniz.
3. Bir veya daha fazla filtre özellikleri ekleyin. Örneğin, belirli bir ülke veya bölgedeki kullanıcılar üzerinde odaklanabilirsiniz. Tıklatın **güncelleştirme** hello filtreleri ayarladıktan sonra. 
4. Merhaba genel saklama grafik kullanıcı bekletme özetini süre seçili hello arasında gösterir. 
5. Merhaba kılavuz according toohello Sorgu Oluşturucu #2'hello sayısı, kullanıcı korunur gösterir. Her satır, dönem gösterilen hello zaman içinde herhangi bir olay gerçekleştiren bir kohort kullanıcıların temsil eder. Merhaba satırdaki her hücre en az bir kez daha sonraki bir süre içinde bu kohort kaç döndürülen gösterir. Bazı kullanıcılar, birden fazla dönemde döndürebilir. 
6. Merhaba Öngörüler kartları üst beş başlatma olaylarını göstermek ve daha iyi anlamak kendi saklama raporun üst beş olayları toogive kullanıcı döndürdü. 

![Bekletme fare vurgulu](./media/app-insights-usage-retention/hover.png)

Kullanıcıların hücreleri hello bekletme aracı tooaccess hello analytics düğmesine üzerine getirin ve hangi hello hücre açıklayan araç ipuçları anlamına gelir. Merhaba Analytics düğmesi kullanıcılar toohello analiz aracı önceden doldurulmuş haldedir sorgu toogenerate kullanıcılarla hello hücreden alır. 

## <a name="use-business-events-tootrack-retention"></a>İş olayları tootrack bekletme kullanın

tooget hello en yararlı bekletme analiz, önemli iş faaliyetlerine temsil eden ölçü olaylar. 

Örneğin, çok sayıda kullanıcı görüntülediği hello oyuna olmadan bir sayfa uygulamanızda açılabilir. Yalnızca hello sayfa görünümleri izleme yanlış tahminidir kaç kişinin, daha önce keyfini sonra hello oyun tooplay dönün, bu nedenle sağlar. tooget oynatıcıları döndürme NET bir resim, uygulamanızı bir kullanıcı gerçekte yürütürken özel bir olay göndermesi gerekir.  

Bu anahtar iş eylemleri temsil eder ve bu bekletme çözümleme için kullanmak iyi bir uygulama toocode özel olayları gösterir. toocapture hello oyun sonucu, toowrite kod toosend özel olay tooApplication Öngörüler kolu gerekir. Merhaba web sayfası koduna veya Node.JS yazma, şuna benzer:

```JavaScript
    appinsights.trackEvent("won game");
```

ASP.NET sunucusu kod:

```C#
   telemetry.TrackEvent("won game");
```

[Özel olaylar yazma hakkında daha fazla bilgi](app-insights-api-custom-events-metrics.md#trackevent).


## <a name="next-steps"></a>Sonraki adımlar
- tooenable kullanımı deneyimleri, göndermeye Başla [özel olaylar](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) veya [sayfa görünümleri](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Özel olaylar ya da sayfa görünümleri keşfedin hello kullanım araçları toolearn zaten gönderirseniz kullanıcılar hizmetinizi kullanma.
    - [Kullanıcılar, Oturumlar, Etkinlikler](app-insights-usage-segmentation.md)
    - [Huniler](usage-funnels.md)
    - [Kullanıcı Akışları](app-insights-usage-flows.md)
    - [Çalışma kitapları](app-insights-usage-workbooks.md)
    - [Kullanıcı bağlamı Ekle](app-insights-usage-send-user-context.md)


