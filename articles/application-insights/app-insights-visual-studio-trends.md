---
title: "Visual Studio aaaAnalyzing eğilimlerini | Microsoft Docs"
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
ms.openlocfilehash: 5c623ec040363f05e80ca927dc8855eb016adc99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyzing-trends-in-visual-studio"></a>Visual Studio Eğilimlerini Çözümleme
Merhaba Application Insights eğilimleri Aracı nasıl web uygulamanızın önemli telemetri olaylarının zaman içinde sorunları ve anormallikleri hızlıca belirlemenize yardımcı değiştiğini gösterir. Toomore bağlayarak ayrıntılı tanılama bilgileri, eğilimler, uygulamanızın performansı, hello özel durumların nedenlerini izlemenize ve özel olaylarınızı ilişkin bilgiler ortaya çıkarmaya yardımcı olabilir.

![Örnek Eğilimler penceresi](./media/app-insights-visual-studio-trends/app-insights-trends-hero-750.png)

## <a name="configure-your-web-app-for-application-insights"></a>Web uygulamanızı Application Insights için yapılandırma

Henüz yapmadıysanız [web uygulamanızı Application Insights için yapılandırın](app-insights-overview.md). Bu toosend telemetri toohello Application Insights portalındaki izin verir. Merhaba eğilimleri aracı hello telemetri buradan okur.

Application Insights Eğilimleri, Visual Studio 2015 Güncelleştirme 3 ve sonrasında mevcuttur.

## <a name="open-application-insights-trends"></a>Application Insights Eğilimleri’ni açma
tooopen hello Application Insights eğilimleri penceresini:

* Merhaba Application Insights araç çubuğu düğmesinden seçin **Telemetri eğilimlerini keşfet**, veya
* Merhaba proje kısayol menüsünden seçin **Application Insights > Telemetri eğilimlerini keşfet**, veya
* Merhaba Visual Studio menü çubuğundan seçin **Görünüm > Diğer Pencereler > Application Insights eğilimleri**.

Bir komut istemi tooselect kaynak görebilirsiniz. Tıklatın **bir kaynak seçin**, bir Azure aboneliği oturum, sonra da Application Insights kaynağı için gibi tooanalyze telemetri eğilimlerini hello listeden seçin.

## <a name="choose-a-trend-analysis"></a>Eğilim analizi seçme
![Eğilim analizi genel türleri menüsü](./media/app-insights-visual-studio-trends/app-insights-trends-1-750.png)

Beş genel eğilim analizinden hello son 24 saat verilerini çözümleyen her birini seçerek işe başlayın:

* **Sunucu isteklerinizin performans sorunlarını araştırmak** -yanıt sürelerine göre gruplandırılan tooyour hizmet istekleri
* **Sunucu isteklerinizdeki hataları çözümleyin** -yapılan HTTP yanıt koduna göre gruplandırılan tooyour hizmet istekleri
* **Uygulamanızdaki Hello özel durumları inceleyin** -hizmetinizde özel durumlar özel durum türüne göre gruplandırılmış
* **Merhaba uygulama bağımlılıklarınızın performansını denetleyin** -hizmetiniz tarafından adlandırılan hizmetleri yanıt sürelerine göre gruplandırılan
* **Özel olaylarınızı inceleyin** - Hizmetiniz için ayarladığınız ve olay türüne göre gruplandırılan özel olaylar.

Önceden oluşturulmuş Bu çözümlemeler daha sonra hello kullanılabilir **sık kullanılan telemetri analizi türlerini görüntüleyin** hello eğilimler penceresinin hello sol üst köşesindeki düğmesi.

## <a name="visualize-trends-in-your-application"></a>Uygulamanızdaki eğilimleri görselleştirme
Application Insights Eğilimleri, uygulamanızın telemetrisinden bir zaman dizisi görselleştirmesi oluşturur. Her bir zaman dizisi görselleştirmesi bir telemetri türünü, ilgili telemetrinin bir özelliğine göre gruplandırarak ve bir zaman aralığı üzerinde gösterir. Örneğin, bunlar, son 24 saat hello kaynaklandığı hello ülkeye göre gruplandırılmış tooview sunucu istekleri isteyebilirsiniz. Bu örnekte, bir saat boyunca hello sunucu istekleri için bazı ülke/bölge sayısı hello görselleştirme üzerindeki her Kabarcık temsil eder.

Hangi telemetri türlerini görüntüleyin hello penceresi tooadjust hello üstünde Hello denetimleri kullanın. İlk olarak, hangi ilgilendiğiniz hello telemetri türlerini seçin:

* **Telemetri Türü** - Sunucu istekleri, özel durumlar, bağımlılıklar veya özel olaylar
* **Zaman aralığı** - arasında herhangi bir yer hello son 30 dakika toohello son 3 gün
* **Gruplandırma Ölçütü** - Özel durum türü, sorun kimliği, ülke/bölge ve daha fazlası.

Ardından **Telemetriyi Çözümle** toorun hello sorgu.

toonavigate hello görselleştirme baloncuklar arasında:

* Tooselect hello filtreleri hello pencerenin altındaki belirli bir süre içinde oluşan yalnızca hello olayları özetlemeye Merhaba, güncelleştirmeleri bir kabarcık tıklatın
* Kabarcık toonavigate toohello arama aracı çift tıklayın ve tüm bu süre içinde oluşan hello telemetri olaylarını tek tek görmek
* CTRL tuşuna basıp tıklayın Kabarcık toode-select hello görselleştirme içinde.

> [!TIP]
> Eğilimler ve arama hello araçları, sabitleme hello sorunların nedenlerini binlerce telemetri olayı arasından hizmetinizdeki toohelp birlikte çalışır. Örneğin, bir öğleden sonra müşterileriniz uygulamanızın daha az yanıt verdiğini fark ederse Eğilimler ile çalışmaya başlayın. Tooyour hizmeti, yanıt süresine göre gruplandırılmış son birkaç saat hello yapılan istekleri analiz edin. Olağan dışı derecede büyük bir yavaş istekler kümesi olup olmadığına bakın. Ardından, Kabarcık toogo toohello arama aracı, filtrelenmiş toothose isteği olayları çift tıklayın. Arama aracında bu isteklerin içeriklerini hello araştırın ve toohello kodu gidin dahil tooresolve hello sorun.
> 
> 

## <a name="filter"></a>Filtre
Merhaba penceresinin alt kısmındaki hello hello filtre denetimleri ile daha özel eğilimleri bulur. tooapply bir filtre adına tıklayın. Hızla bir belirli telemetrinizin içinde gizleme farklı filtreler toodiscover eğilimleri arasında geçiş yapabilirsiniz. Özel durum türü gibi bir boyuttaki bir filtre uygularsanız, diğer yönlerdeki filtreler grileştirilmiş görünse bile tıklanabilir kalır. tooun-bir filtre uygulamak için yeniden tıklayın. CTRL tuşuna basıp tıklayın tooselect birden çok filtre hello aynı boyut.

![Eğilim filtreleri](./media/app-insights-visual-studio-trends/TrendsFiltering-750.png)

Ne tooapply birden çok filtre istiyorsunuz? 

1. Merhaba ilk filtreyi uygulayın. 
2. Merhaba tıklatın **seçili Filtreleri Uygula ve yeniden sorgula** birinci filtrenizin hello boyutunun hello adıyla düğmesi. Bunun yapılması telemetrinizi yalnızca hello birinci filtreyle eşleşen olaylar için yeniden sorgular. 
3. İkinci bir filtre uygulayın. 
4. Merhaba işlem toofind belirli alt eğilimler yineleyin. Örneğin, adı "GET Home/Index" olan *ve* Almanya’dan gelen *ve* 500 yanıt kodu alan sunucu istekleri. 

tooun-bu filtrelerden birini uygulamak istiyorsanız hello tıklayın **seçili filtreleri Kaldır ve yeniden sorgula** hello boyut düğmesi.

![Birden fazla filtre](./media/app-insights-visual-studio-trends/TrendsFiltering2-750.png)

## <a name="find-anomalies"></a>Anormallikleri bulma
Merhaba eğilimleri aracı anormal karşılaştırılan tooother balonları hello içinde olayları balonları vurgulayın aynı zaman serisi. Merhaba görünüm türü açılır listesinde seçin **zaman aralığındaki yüzdeler (anomalileri vurgula) içinde sayar** veya **zaman aralığındaki yüzdeler (anomalileri vurgula)**. Kırmızı baloncuklar anormaldir. Anormallikleri sayıları/yüzdeleri hello (Merhaba görüntülüyorsanız 48 saat son 24 saatte bir vb.) iki dönemleri geçmiş oluştu hello sayıları/yüzdeleri standart sapmasının 2.1 katını aşan hello ile baloncuklar olarak tanımlanır.

![Renkli noktalar anomalileri gösterir](./media/app-insights-visual-studio-trends/TrendsAnomalies-750.png)

> [!TIP]
> Anomalilerin vurgulanması özellikle diğer durumlarda benzer şekilde boyutlandırılabilecek küçük baloncukların zaman dizisindeki aykırı değerlerini bulmak için yararlıdır.  
> 
> 

## <a name="next"></a>Sonraki adımlar
|  |  |
| --- | --- |
| **[Visual Studio’da Application Insights ile çalışma](app-insights-visual-studio.md)**<br/>Telemetri arayın, CodeLens içindeki verilere bakın ve Application Insights’ı yapılandırın. Hepsi Visual Studio’da. |![Merhaba projesine sağ tıklayın ve Application Insights seçme arama](./media/app-insights-visual-studio-trends/34.png) |
| **[Daha fazla veri ekleme](app-insights-asp-net-more.md)**<br/>Kullanımı, kullanılabilirliği, bağımlılıkları, özel durumları izleyin. Günlük altyapılarından izlemeleri tümleştirin. Özel telemetri yazın. |![Visual studio](./media/app-insights-visual-studio-trends/64.png) |
| **[Merhaba Application Insights portalıyla çalışma](app-insights-dashboards.md)**<br/>Panolar, güçlü tanılama ve analiz araçları, uyarılar, uygulamanızın canlı bağımlılık haritası ve telemetriyi dışarı aktarma. |![Visual studio](./media/app-insights-visual-studio-trends/62.png) |

