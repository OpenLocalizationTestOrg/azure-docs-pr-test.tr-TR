---
title: "Azure Application Insights web uygulaması performans değişikliklerin aaaSmart tanılama | Microsoft Docs"
description: "Otomatik tanılama ani veya performans telemetrisini adımlarda web uygulamanızdan."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: cfreeman
ms.openlocfilehash: 8891762c4a4bfdb08b647fe3b702349eb30ec9c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a>Uygulama telemetrinizi ani değişiklikler tanılama

*Bu özelliğin önizlemede değil.*

Web uygulamanızın performansı veya tek bir tıklatmayla kullanımı ani değişiklikler tanılamak! Merhaba akıllı Tanılama özelliğini, her zaman grafik oluşturduğunuzda kullanılabilir [Analytics](app-insights-analytics.md) içinde [Application Insights](app-insights-overview.md). Bir depo veya bir DIP gibi sonuçlarınızı hello eğilimini olağan dışı bir değişiklik olduğunda akıllı tanılama bir desen boyutları ve hello değişiklik açıklayabilir ilgili değerleri tanımlar. Bu, hızlı bir şekilde hello sorunu tanılamak yardımcı olur. 

Bu örnekte, akıllı tanılama hello değişiklikle ilişkili özellik değerlerinin bir desen belirledi ve sonuçları ile ve bu deseni olmadan hello birbirinden vurgular:

![Örnek analytics Tanılama sonucu](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a>Veri değişikliklerini tanılama

1.  Analizleri bir sorgu çalıştırın ve zaman grafik olarak işleme. 
2.  Varsa herhangi bir vurgulanan yoğun noktasını'ı tıklatın.
 
    ![yoğun noktası](./media/app-insights-analytics-diagnostics/peak.png)

    Tanılama birkaç saniye sürer toodiscover bir desen.

3. Merhaba Tanılama sonuçları sekmesi, veri süreksizlik açıklayabilir bir desen gösterir.

    ![Sonuç](./media/app-insights-analytics-diagnostics/result.png)
 
    Merhaba metni hello shift ile toocorrelate görünür hello boyut değerleri gösterir. Bu örnekte, belirli bir istek ve belirli tarayıcı sürümü ile ilişkili.

    Ayrıca hello grafikle hello filtre true ve false hello iki bileşenlerinin dikkat edin. Merhaba false bileşen değişmeden eğilimi gösterir. Diğer bir deyişle, biz hello sorunlu birleşimlerini tanılama tanımladığı bıraksanız hello telemetri sonuçlarında değişiklik yoktur. Bunun aksine, bu bileşimi içinde hello sonuçları çarpıcı değişiklik gösterir ve bu da araştırma vurgulanmış hello alanı içinde. Bu tanılama hello değişiklik açıklayan özellikleri bileşimini buldu gösterir.

4.  Merhaba düzeni karmaşıksa toohover üzerinden ihtiyacınız **Tümünü Göster** toosee hello boyutları.

    ![tümünü göster](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  Hiçbir önemli düzeni toonotify 'sonuç' sayfa sunulur hello hakkında tanılama bulur durumda. Bu noktada, sorgunuzu değişebilir. Örneğin, hello zaman aralığı ve daha fazla çözümleme ve potansiyel olarak daha iyi sonuçlar için Analytics sorgu binning daraltabilirsiniz.

Web sitenizin belirli bir sayfa üzerinde belirli bir tarayıcı bir sorun olduğunu hello bilen sayesinde artık düz toohello sorun sayfasına gidin ve en son değişiklikler araştırın.

## <a name="try-hello-demo"></a>Merhaba Tanıtımı deneyin

[Toosee Tanıtımı burayı](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) örnek verileri.

## <a name="how-it-works"></a>Nasıl çalışır?

Akıllı tanılama üzerinde hello dayalı bir Gelişmiş Denetimsiz machine learning algoritmasını kullanan [DiffPatterns](app-insights-analytics-reference.md) işlemi. Merhaba veri değişikliği açıklayabilir için aday desenleri görünüyor. Her adayı hello ölçüm üzerindeki etkisini hello analizleri yaparken ve en iyi hello değişiklikle karşılık gelen hello deseni gösterir.

## <a name="no-diagnostic-points"></a>Tanılama noktası yok?

Ölçüt aşağıdaki hello sağlandığında akıllı tanılama yalnızca çalışır:

 * Akıllı tanılama ayarını açık. Merhaba ayarlar simgesine analytics'te kısmına bakın.
 * Merhaba analizi ayarları akıllı tanılama seçeneğinde seçilir. 
 * Zaman ekseni: hello hello grafiğin x ekseni türde olmalıdır `datetime`.
 * Çizgi veya alan grafiği: Tanılama yalnızca bu tür grafik çalışır. Kullanım `| render timechart` veya `| render areachart` ; sorgunuzu hello sonunda veya satır ya da alan grafiği hello açılan seçicisini seçin.
 * Süreksizlik: Hello verilerde önemli süreksizlik koyulmalıdır.
 * Yeterli noktaları tooanalyze.
 * Birden fazla hello sorgu yan tümcesinde özetler.
 * Merhaba önce adı tanımını içeren hiçbir proje yan tümcesi özetler.

 
 ## <a name="related-articles"></a>İlgili makaleler

 * [Analytics Öğreticisi](app-insights-analytics-tour.md)
 * [Akıllı algılama](app-insights-proactive-diagnostics.md) tooperformance sorunları otomatik olarak sizi uyarır.
