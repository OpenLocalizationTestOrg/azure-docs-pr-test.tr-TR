---
title: "aaaAzure ASP.NET Core için Application Insights | Microsoft Docs"
description: "Kullanılabilirlik, performans ve kullanım için Web uygulamalarını izleyin."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 3b722e47-38bd-4667-9ba4-65b7006c074c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: a7a27f9eef1daec5b0deae9fd88906e646980659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-aspnet-core"></a>ASP.NET Core için Application Insights
[Application Insights](app-insights-overview.md) , web uygulamanızın kullanılabilirlik, performans ve kullanım izlemenize izin verir. Merhaba performans ve hello uygulamanızda verimliliğini hakkında joker elde hello geri bildirim ile her geliştirme yaşam döngüsündeki hello tasarım hello yönünü hakkında bilinçli seçimler yapabilirsiniz.

![Örnek](./media/app-insights-asp-net-core/sample.png)

Bir aboneliğe gerekir [Microsoft Azure](http://azure.com). Windows, XBox Live veya diğer Microsoft bulut hizmetlerinde kullanıyor olabileceğiniz bir Microsoft hesabıyla oturum açın. Takımınızın Kurumsal abonelik tooAzure sahip olabilir: hello sahibi tooadd isteyin Microsoft hesabınızı kullanarak tooit.

## <a name="getting-started"></a>Başlarken

* Visual Studio Çözüm Gezgini'nde, projenize sağ tıklayın ve seçin **yapılandırma Application Insights**, veya **Ekle > Application Insights**. [Daha fazla bilgi edinin](app-insights-asp-net.md).
* Bu menü komutlarını görmüyorsanız hello izleyin [alma Başlarken Kılavuzu](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started). Projeniz Visual Studio sürümü ile 2017 önce oluşturulduysa, bu toodo gerekebilir.

## <a name="using-application-insights"></a>Application Insights’ı Kullanma
Merhaba içine oturum [Microsoft Azure portal](https://portal.azure.com)seçin **tüm kaynakları** veya **Application Insights**ve ardından uygulamanızı toomonitor oluşturulan hello kaynağı seçin.

Ayrı bir tarayıcı penceresinde uygulamanızı biraz kullanın. Merhaba Application Insights grafikte görüntülenen verileri görürsünüz. (Tooclick yenileme sahip olabilir.) Geliştirme yapıyorsanız sırasında yalnızca küçük miktarda veri olacaktır, ancak uygulamanızı yayınlama ve çok sayıda kullanıcı varsa bu grafikler gerçekten Canlı gelir. 

Merhaba genel bakış sayfasında anahtar performans grafiklerini gösterir: sunucu yanıt süresi, sayfa yükleme süresi ve başarısız isteklerin sayısı. Daha fazla grafikler ve veri herhangi grafik toosee tıklayın.

Merhaba portal görünümlerde üç ana kategoriye ayrılır:

* [Ölçüm Gezgini](app-insights-metrics-explorer.md) oluşturduğunuz kendiniz ile Merhaba grafikleri ve ölçümleri ve yanıt sürelerini, başarısızlık oranları veya ölçümleri gibi sayıları tabloları gösterir [API](app-insights-api-custom-events-metrics.md). Daha iyi uygulamanızı ve kullanıcılarına anlamak özellik değerleri tooget tarafından filtre ve segment hello verileri.
* [Arama Gezgini](app-insights-diagnostic-search.md) belirli istekleri, özel durumlar, günlük izlemelerini ya da oluşturduğunuz kendiniz hello ile olayları gibi olayları tek tek listeler [API](app-insights-api-custom-events-metrics.md). Filtre hello olayları aramak ve ilgili olaylar tooinvestigate sorunları arasında gidin.
* [Analytics](app-insights-analytics.md) siz telemetrinize SQL benzeri sorguları çalıştırmak sağlar ve güçlü bir Analitik ve tanı aracıdır.

## <a name="alerts"></a>Uyarılar
* Otomatik olarak Al [öngörülü tanılama uyarıları](app-insights-proactive-diagnostics.md) , belirtilir başarısızlık oranları ve diğer ölçümleri anormal değişiklikler hakkında.
* Ayarlanan [kullanılabilirlik testleri](app-insights-monitor-web-app-availability.md) Web sitenizi sürekli olarak dünya çapında konumları ve get herhangi başarısız test hemen sonra e-postalar tootest.
* Ayarlanan [ölçüm uyarıları](app-insights-monitor-web-app-availability.md) ölçümleri yanıt sürelerini veya özel durum oranları gibi dış kabul edilebilir sınırlar giderseniz tooknow.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a>Açık kaynak
[Okuma ve toohello kodu katkıda bulunan](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a>Sonraki adımlar
* [Telemetri tooyour web sayfaları eklemek](app-insights-javascript.md) toomonitor sayfa kullanım ve performans.
* [İzleme bağımlılıkları](app-insights-asp-net-dependencies.md) REST, SQL veya diğer dış kaynaklara, yavaşlamadan varsa toosee.
* [Merhaba API kullanan](app-insights-api-custom-events-metrics.md) toosend kendi olayları ve ölçümleri, uygulamanızın performansı ve kullanımı daha ayrıntılı bir görünüm için.
* [Kullanılabilirlik testleri](app-insights-monitor-web-app-availability.md) uygulamanızdan sürekli Merhaba Dünya denetleyin. 

