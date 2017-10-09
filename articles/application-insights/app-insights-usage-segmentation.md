---
title: Azure Application Insights aaaUser, oturum ve olay analizi | Microsoft docs
description: "Kullanıcılar, web uygulamanızın demografik analizini."
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
ms.openlocfilehash: 152ab90e9a25c03087d3ebbde1263ec72acb227e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a>Application Insights kullanıcıları, oturumlar ve olayları çözümleme

Kişilerin web uygulamanızı kullandığınızda, bunlar en, kullanıcılarınızın bulunduğu ilgileniyor hangi sayfaların, hangi tarayıcılar ve işletim sistemleri bunlar kullandığını öğrenin. İş ve kullanım telemetrisi kullanarak çözümlemek [Azure Application Insights](app-insights-overview.md).

## <a name="get-started"></a>başlarken

Merhaba kullanıcıları, oturumları veya olayları Kanatlar hello Application Insights portalında verileri henüz görmüyorsanız, [tooget hello kullanım araçları ile çalışmaya nasıl bilgi](app-insights-usage-overview.md).

## <a name="hello-users-sessions-and-events-segmentation-tool"></a>Merhaba kullanıcıları, oturumlar ve Olayları kesimleme aracı

Üç perspektiflerden web uygulamanızdan aynı aracı tooslice ve bölmek telemetrinin hello üç hello kullanım Kanatlar kullanın. Filtreleme ve hello veri bölme hello göreli ve kullanımı için farklı sayfalar özellikleri hakkında Öngörüler açığa.

* **Kullanıcılar aracını**: kaç kişinin uygulamanızı ve özelliklerini kullanılır.  Kullanıcıların, tarayıcı tanımlama bilgilerinde depolanan anonim kimlikleri kullanılarak sayılır. Farklı tarayıcılar ya da makineleri kullanan tek bir kişi olarak birden fazla kullanıcı sayılacaktır.
* **Oturumlar aracını**: kullanıcı etkinliği kaç oturumları belirli sayfalarını ve özelliklerini, uygulamanızın eklediniz. Bir oturum kullanım sürekli 24 h veya kullanıcı yapılmadıktan yarım saat sonra sayılır.
* **Olayları aracı**: belirli sayfalarını ve özelliklerini, uygulamanızın ne sıklıkta kullanılır. Sahip olduğunuz sağlanan sayfa görünümü bir tarayıcı, uygulamanızdan bir sayfa yüklediğinde sayılır [onu izlenmiş](app-insights-javascript.md). 

    Özel bir olay şeyin uygulamanızda bir düğmeyi tıklatın veya bazı görev tamamlanmasından hello gibi genellikle bir kullanıcı etkileşimi bir oluşumu temsil eder. Kodu, uygulamanızda çok eklediğiniz[özel olayları](app-insights-api-custom-events-metrics.md#trackevent).

![Kullanım aracı](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a>Belirli kullanıcıların sorgulama 

Farklı kullanıcı grupları hello kullanıcılar aracını hello üstündeki hello sorgu seçeneklerini ayarlayarak keşfedin: 

* Kim: özel olaylar seçin ve sayfa görünümleri. 
* İşlem sırasında: bir zaman aralığı seçin. 
* : Tarafından nasıl toobucket hello verileri, bir süre veya tarayıcı veya şehir gibi başka bir özellik seçin. 
* Bölme: bir özellik tarafından toosplit veya segment hello veri seçin. 
* Filtreler ekleyin: hello sorgusu toocertain kullanıcıları, oturumları veya olayları, tarayıcı veya şehir gibi özelliklerine göre sınırlayın. 
 
## <a name="saving-and-sharing-reports"></a>Kaydetme ve raporları paylaşma 
Kullanıcıların raporları, hello raporlarım bölümünde, özel ya da yalnızca tooyou kaydedebilir veya erişim toothis Application Insights kaynağı başka herkesle hello paylaşılan raporları bölümüne paylaşılan.  
 
Raporu kaydetme veya özelliklerini düzenlerken, bazı sabit süreyi geri dönerseniz verilerin, bir rapor sürekli olacak "Geçerli göreli zaman aralığı" toosave yenilenmesi seçin.  
 
"Geçerli mutlak zaman aralığı" toosave sabit bir veri kümesiyle bir rapor seçin. Application Insights verileri yalnızca 90 90 günden itibaren mutlak zaman aralığı olan bir raporu geçmişse kaydedildiği şekilde gün süreyle depolanır unutmayın, hello rapor boş görünür. 
 
## <a name="example-instances"></a>Örnek örnekleri

Merhaba örnek örnekleri bölümüne sayıda bireysel kullanıcıları, oturumları veya hello geçerli sorgu tarafından eşleşen olaylar hakkında bilgi gösterir. Dikkate ve toplama tooaggregates içinde kişiler hello davranışlarını keşfetme kişiler gerçekten uygulamanızı kullanma hakkında bilgiler sağlar. 
 
## <a name="insights"></a>Insights 

Merhaba Öngörüler kenar ortak özellikleri paylaşır kullanıcılar büyük kümelerini gösterir. Bu kümeleri kişiler uygulamanızı kullanma şaşırtıcı eğilimleri ortaya çıkarmaya. Örneğin, tüm, uygulamanızın hello kullanımı % 40 tek bir özelliğini kullanarak kişilerden geliyorsa.  


## <a name="next-steps"></a>Sonraki adımlar
- tooenable kullanımı deneyimleri, göndermeye Başla [özel olaylar](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) veya [sayfa görünümleri](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Özel olaylar ya da sayfa görünümleri keşfedin hello kullanım araçları toolearn zaten gönderirseniz kullanıcılar hizmetinizi kullanma.
    - [Huniler](usage-funnels.md)
    - [Bekletme](app-insights-usage-retention.md)
    - [Kullanıcı Akışları](app-insights-usage-flows.md)
    - [Çalışma kitapları](app-insights-usage-workbooks.md)
    - [Kullanıcı bağlamı Ekle](app-insights-usage-send-user-context.md)

