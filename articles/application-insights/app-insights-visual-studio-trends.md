---
title: "Visual Studio Eğilimlerini Çözümleme | Microsoft Docs"
description: "Visual Studio Application Insights telemetri eğilimlerini çözümleyin, görselleştirin ve keşfedin."
services: application-insights
documentationcenter: .net
author: numberbycolors
manager: carmonm
ms.assetid: 3150c6fc-2691-44f6-a290-fc5cd68e692a
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: 13fca37303296355ce601333b13110d04fa5fa4e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="analyzing-trends-in-visual-studio"></a>Visual Studio Eğilimlerini Çözümleme
Application Insights Eğilimleri aracı, web uygulamanızın önemli telemetri olaylarının zaman içinde nasıl değiştiğini gösterir ve sorunları ve anormallikleri hızlıca belirlemenize yardımcı olur. Sizi daha ayrıntılı tanılama bilgilerine bağlayan Eğilimler, uygulamanızın performansını geliştirmenize, özel durumların nedenlerini izlemenize ve özel olaylarınıza ilişkin bilgileri açığa çıkarmanıza yardımcı olabilir.

![Örnek Eğilimler penceresi](./media/app-insights-visual-studio-trends/app-insights-trends-hero-750.png)

## <a name="configure-your-web-app-for-application-insights"></a>Web uygulamanızı Application Insights için yapılandırma

Henüz yapmadıysanız [web uygulamanızı Application Insights için yapılandırın](app-insights-overview.md). Bunun yapılması, Application Insights portalına telemetri gönderilmesine olanak tanır. Eğilimler aracı, telemetriyi buradan okur.

Application Insights Eğilimleri, Visual Studio 2015 Güncelleştirme 3 ve sonrasında mevcuttur.

## <a name="open-application-insights-trends"></a>Application Insights Eğilimleri’ni açma
Application Insights Eğilimleri penceresini açmak için:

* Application Insights araç çubuğu düğmesinden **Telemetri Eğilimlerini Keşfet**’i seçin veya
* Proje kısayol menüsünden **Application Insights > Telemetri Eğilimlerini Keşfet**’i seçin veya
* Visual Studio menü çubuğundan **Görünüm > Diğer Pencereler > Application Insights Eğilimleri**’ni seçin.

Kaynak seçmenizi isteyen bir ileti görebilirsiniz. **Kaynak seç** öğesine tıklayın, bir Azure aboneliği ile oturum açın, ardından listeden telemetri eğilimlerini çözümlemek istediğiniz bir Application Insights kaynağını seçin.

## <a name="choose-a-trend-analysis"></a>Eğilim analizi seçme
![Eğilim analizi genel türleri menüsü](./media/app-insights-visual-studio-trends/app-insights-trends-1-750.png)

Her biri son 24 saatin verilerini çözümleyen beş genel eğilim analizinden birini seçerek işe başlayın:

* **Sunucu isteklerinizin performans sorunlarını denetleyin** - Hizmetinize yapılan ve yanıt sürelerine göre gruplandırılan istekler
* **Sunucu isteklerinizdeki hataları çözümleyin** - Hizmetinize yapılan ve HTTP yanıt koduna göre gruplandırılan istekler
* **Uygulamanızdaki özel durumları inceleyin** - Hizmetinizde özel durum türüne göre gruplandırılmış özel durumlar
* **Uygulama bağımlılıklarınızın performansını denetleyin** - Hizmetiniz tarafından çağrılan ve yanıt sürelerine göre gruplandırılan hizmetler
* **Özel olaylarınızı inceleyin** - Hizmetiniz için ayarladığınız ve olay türüne göre gruplandırılan özel olaylar.

Önceden oluşturulmuş bu çözümlemeler Eğilimler penceresinin sol üst köşesindeki **Sık kullanılan telemetri analizi türlerini görüntüleyin** düğmesinden kullanılabilir.

## <a name="visualize-trends-in-your-application"></a>Uygulamanızdaki eğilimleri görselleştirme
Application Insights Eğilimleri, uygulamanızın telemetrisinden bir zaman dizisi görselleştirmesi oluşturur. Her bir zaman dizisi görselleştirmesi bir telemetri türünü, ilgili telemetrinin bir özelliğine göre gruplandırarak ve bir zaman aralığı üzerinde gösterir. Örneğin, oluşturuldukları ülkeye göre gruplandırılmış son 24 saatteki sunucu isteklerini görüntülemek isteyebilirsiniz. Bu örnekte görselleştirme üzerindeki her baloncuk bir saat boyunca belirli bir ülke/bölge için yapılan sunucu isteklerinin sayısını gösterir.

Hangi telemetri türlerini görüntüleyeceğinizi ayarlamak için pencerenin üstündeki denetimleri kullanın. İlk olarak ilgilendiğiniz telemetri türlerini seçin:

* **Telemetri Türü** - Sunucu istekleri, özel durumlar, bağımlılıklar veya özel olaylar
* **Zaman Aralığı** - Son 30 dakika ile son 3 gün arasında herhangi bir yer
* **Gruplandırma Ölçütü** - Özel durum türü, sorun kimliği, ülke/bölge ve daha fazlası.

Ardından, sorguyu çalıştırmak için **Telemetriyi Çözümle**’ye tıklayın.

Görseldeki baloncuklar arasında gezinmek için:

* Bir baloncuğa tıklayarak seçtiğinizde pencerenin altındaki filtreler güncelleştirilir ve yalnızca belirli bir süre içinde oluşan olaylar özetlenir
* Arama aracında gezinmek için bir baloncuğa çift tıklayın ve ilgili süre içinde gerçekleşen tüm telemetri olaylarını tek tek görüntüleyin
* Baloncuğun görseldeki seçimini kaldırmak için Ctrl tuşuna basıp tıklayın.

> [!TIP]
> Eğilimler ve Arama araçları, binlerce telemetri olayı arasından hizmetinizdeki sorunların nedenlerini belirlemenize yardımcı olmak üzere birlikte çalışır. Örneğin, bir öğleden sonra müşterileriniz uygulamanızın daha az yanıt verdiğini fark ederse Eğilimler ile çalışmaya başlayın. Son birkaç saat içinde hizmetinize yapılan istekleri, yanıt süresine göre gruplandırılmış halde çözümleyin. Olağan dışı derecede büyük bir yavaş istekler kümesi olup olmadığına bakın. Ardından baloncuğa çift tıklayarak Arama aracına gidin ve bu istek olaylarını filtreleyin. Arama aracında bu isteklerin içeriklerini keşfedebilir ve sorunu çözmek için ilgili koda gidebilirsiniz.
> 
> 

## <a name="filter"></a>Filtre
Pencerenin altındaki filtre denetimleri ile daha özel eğilimleri bulun. Bir filtre uygulamak için adına tıklayın. Telemetrinizin belirli bir yönünde gizlenmiş olabilecek eğilimleri bulmak için farklı filtreler arasında hızlıca geçiş yapabilirsiniz. Bir yönde Özel Durum Türü gibi bir filtre uygularsanız, diğer yönlerdeki filtreler grileştirilmiş görünse bile tıklanabilir durumda kalır. Bir filtrenin uygulamasını kaldırmak için filtreye yeniden tıklayın. Aynı yönde birden fazla filtreyi seçmek için Ctrl tuşuna basıp tıklayın.

![Eğilim filtreleri](./media/app-insights-visual-studio-trends/TrendsFiltering-750.png)

Birden fazla filtre uygulamak isterseniz ne olur? 

1. İlk filtreyi uygulayın. 
2. Birinci filtrenizin yön adının yanındaki **Seçili filtreleri uygula ve yeniden sorgula** düğmesine tıklayın. Bunun yapılması telemetrinizi yalnızca birinci filtreyle eşleşen olaylar için yeniden sorgular. 
3. İkinci bir filtre uygulayın. 
4. Telemetrinizin belirli alt kümelerindeki eğilimleri bulmak için işlemi tekrarlayın. Örneğin, adı "GET Home/Index" olan *ve* Almanya’dan gelen *ve* 500 yanıt kodu alan sunucu istekleri. 

Bu filtrelerden birini kaldırmak için yöne ilişkin **Seçili filtreleri kaldır ve yeniden sorgula** düğmesine tıklayın.

![Birden fazla filtre](./media/app-insights-visual-studio-trends/TrendsFiltering2-750.png)

## <a name="find-anomalies"></a>Anormallikleri bulma
Eğilimler aracı, aynı zaman dizisindeki diğer baloncuklara kıyasla anormal olan olayların baloncuklarını vurgulayabilir. Görünüm Türü açılır listesinde **Zaman aralığındaki sayımlar (anomalileri vurgula)** veya **Zaman aralığındaki yüzdeler (anomalileri vurgula)** seçeneğini belirleyin. Kırmızı baloncuklar anormaldir. Anomaliler sayıları/yüzdeleri, son iki zaman dilimi (örneğin, son 24 saati görüntülüyorsanız 48 saat) boyunca gerçekleşen sayıların/yüzdelerin standart sapmasının 2.1 katını aşan baloncuklar olarak tanımlanır.

![Renkli noktalar anomalileri gösterir](./media/app-insights-visual-studio-trends/TrendsAnomalies-750.png)

> [!TIP]
> Anomalilerin vurgulanması özellikle diğer durumlarda benzer şekilde boyutlandırılabilecek küçük baloncukların zaman dizisindeki aykırı değerlerini bulmak için yararlıdır.  
> 
> 

## <a name="next"></a>Sonraki adımlar
|  |  |
| --- | --- |
| **[Visual Studio’da Application Insights ile çalışma](app-insights-visual-studio.md)**<br/>Telemetri arayın, CodeLens içindeki verilere bakın ve Application Insights’ı yapılandırın. Hepsi Visual Studio’da. |![Projeye sağ tıklayın ve Application Insights, Ara’yı seçin](./media/app-insights-visual-studio-trends/34.png) |
| **[Daha fazla veri ekleme](app-insights-asp-net-more.md)**<br/>Kullanımı, kullanılabilirliği, bağımlılıkları, özel durumları izleyin. Günlük altyapılarından izlemeleri tümleştirin. Özel telemetri yazın. |![Visual studio](./media/app-insights-visual-studio-trends/64.png) |
| **[Application Insights portalıyla çalışma](app-insights-dashboards.md)**<br/>Panolar, güçlü tanılama ve analiz araçları, uyarılar, uygulamanızın canlı bağımlılık haritası ve telemetriyi dışarı aktarma. |![Visual studio](./media/app-insights-visual-studio-trends/62.png) |

