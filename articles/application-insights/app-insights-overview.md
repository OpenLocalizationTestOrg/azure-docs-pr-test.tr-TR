---
title: Azure Application Insights nedir? | Microsoft Belgeleri
description: "Uygulama Performansı Yönetimi ve canlı web uygulamanızın kullanımını izleme.  Sorunları algılayın, önceliklendirin ve tanılayın; kullanıcıların uygulamanızı nasıl kullandığını anlayın."
services: application-insights
documentationcenter: 
author: mrbullwinkle
manager: carmonm
ms.assetid: 379721d1-0f82-445a-b416-45b94cb969ec
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: overview
ms.custom: mvc
ms.date: 05/14/2017
ms.author: mbullwin
ms.openlocfilehash: 2e2a9e8491ad56bcbc42be64729715016f7ed17b
ms.sourcegitcommit: c25cf136aab5f082caaf93d598df78dc23e327b9
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/15/2017
---
# <a name="what-is-application-insights"></a>Application Insights nedir?
Application Insights, farklı platformlardaki web geliştiricilerine yönelik kapsamlı bir Uygulama Performans Yönetimi (APM) hizmetidir. Canlı web uygulamanızı izlemek için kullanabilirsiniz. Performans anormalliklerini otomatik olarak algılar. Sorunları tanılamanıza ve kullanıcıların uygulamanızla aslında neler yaptığını anlamanıza yardımcı olan güçlü analiz araçları içerir.  Performansı ve kullanılabilirliği sürekli geliştirmenize yardımcı olmak amacıyla tasarlanmıştır. .NET, Node.js ve J2EE gibi çok çeşitli platformlarda, şirket içi veya bulutta barındırılan uygulamalar için yararlıdır. DevOps işleminizle tümleştirilir ve çeşitli geliştirme araçlarıyla bağlantı noktaları vardır. Visual Studio App Center ve HockeyApp ile tümleştirerek mobil uygulamalardan telemetriyi izleyebilir ve çözümleyebilir.

![Kullanıcı etkinliği istatistiklerinin grafiğini oluşturun veya belirli olayları ayrıntısına gidin.](./media/app-insights-overview/00-sample.png)

[Giriş animasyonuna göz atın](https://www.youtube.com/watch?v=fX2NtGrh-Y0).

## <a name="how-does-application-insights-work"></a>Application Insights nasıl çalışır?
Uygulamanıza küçük bir izleme paketi yüklersiniz ve Microsoft Azure portalında bir Application Insights kaynağı ayarlarsınız. İzleme aracı uygulamanızı izler ve telemetri verilerini portala gönderir. (Uygulamanın nerede çalıştığı önemli değildir ve Azure’da barındırılması gerekmez.)

Yalnızca web hizmeti uygulamasını değil, tüm arka plan bileşenlerini ve web sayfalarının kendisindeki JavaScript’i de izleyebilirsiniz. 

![Uygulamanızdaki Application Insights izleme aracı, Application Insights kaynağınıza telemetri gönderir.](./media/app-insights-overview/01-scheme.png)


Buna ek olarak performans sayaçları, Azure tanılama veya Docker günlükleri gibi konak ortamlarından da telemetri çekebilirsiniz. Web hizmetinize düzenli aralıklarla yapay istekler gönderen web testleri de ayarlayabilirsiniz.

Bu telemetri akışlarının tamamı Azure portalında tümleştirilir ve burada ham verilere güçlü analiz ve arama araçları uygulayabilirsiniz.


### <a name="whats-the-overhead"></a>Ne kadar ek yük getirir?
Uygulamanızın performansı üzerindeki etkisi çok küçüktür. İzleme çağrıları engelleyici değildir ve toplanarak ayrı bir iş parçacığında gönderilir.

## <a name="what-does-application-insights-monitor"></a>Application Insights neleri izler?

Geliştirme takımına yönelik olan Application Insights, uygulamanızın performansını ve nasıl kullanıldığını anlamanıza yardımcı olur. Şunları izler:

* **İstek oranları, yanıt süreleri ve hata oranları**: Hangi sayfaların günün hangi saatlerinde popüler olduğunu ve kullanıcılarınızın konumunu öğrenin. En iyi performansı hangi sayfaların gösterdiğini görün. Daha fazla istek olduğunda yanıt süreleriniz ve hata oranlarınız yükseliyorsa bir kaynak atama sorununuz olabilir. 
* **Bağımlılık oranları, yanıt süreleri ve hata oranları**: Dış hizmetlerin sizi yavaşlatıp yavaşlatmadığını öğrenin.
* **Özel durumlar**: Toplu istatistikleri analiz edin veya belirli örnekleri seçerek yığın izlemesi ve ilgili isteklerin ayrıntılarına gidin. Hem sunucu hem de tarayıcı özel durumları raporlanır.
* **Sayfa görüntüleme sayısı ve yükleme performansı**: Kullanıcılarınızın tarayıcıları tarafından gerçekleştirilir.
* Web sayfalarından **AJAX çağrıları**: Oranlar, yanıt süreleri ve hata oranları.
* **Kullanıcı ve oturum sayıları**.
* Windows veya Linux sunucu makinelerinizden CPU, bellek ve ağ kullanımı gibi **performans sayaçları**. 
* Docker veya Azure’dan **konak tanılama**. 
* Uygulamanızdan **tanılama izleme günlükleri**: İzleme olayları ile istekler arasında bağıntı kurmanıza imkan tanır.
* Satılan öğeler ya da kazanılan maçlar gibi iş olaylarını izlemek için istemcide ya da sunucu kodunda kendi yazdığınız **özel olaylar ve ölçümler**.

## <a name="where-do-i-see-my-telemetry"></a>Telemetrimi nerede görebilirim?

Verilerinizi keşfetmenin birçok yolu vardır. Aşağıdaki makaleleri inceleyin:

|  |  |
| --- | --- |
| [**Akıllı algılama ve el ile uyarılar**](app-insights-proactive-diagnostics.md)<br/>Otomatik uyarılar, uygulamanızın normal telemetri desenlerine uyum sağlar ve normal desenin dışında bir durum gelişirse tetiklenir. Belirli özel veya standart ölçüm düzeylerinde de [uyarılar](app-insights-alerts.md) ayarlayabilirsiniz. |![Uyarı örneği](./media/app-insights-overview/alerts-tn.png) |
| [**Uygulama eşlemesi**](app-insights-app-map.md)<br/>Uygulamanızın bileşenlerinin yanı sıra önemli ölçüm ve uyarılar. |![Uygulama eşlemesi](./media/app-insights-overview/appmap-tn.png)  |
| [**Profil Oluşturucu**](app-insights-profiler.md)<br/>Örnek isteklerinin yürütme profillerini inceleyin. |![Profil Oluşturucu](./media/app-insights-overview/profiler.png) |
| [**Kullanım analizi**](app-insights-usage-overview.md)<br/>Kullanıcıların segmentlere nasıl ayrıldığını ve nasıl elde tutulduğunu çözümleyin.|![Elde tutma aracı](./media/app-insights-overview/retention.png) |
| [**Örnek verileri için tanılama arama**](app-insights-diagnostic-search.md)<br/>İstekler, özel durumlar, bağımlılık çağrıları, günlük izlemeleri ve sayfa görüntülemeleri gibi olaylarda arama yapın ve bunları filtreleyin.  |![Telemetri arama](./media/app-insights-overview/search-tn.png) |
| [**Toplu veriler için Ölçüm Gezgini**](app-insights-metrics-explorer.md)<br/>İstek, hata ve özel durum oranları; yanıt süreleri, sayfa yükleme süreleri gibi toplu verileri keşfedin, filtreleyin ve bölümlere ayırın. |![Ölçümler](./media/app-insights-overview/metrics-tn.png) |
| [**Panolar**](app-insights-dashboards.md#dashboards)<br/>Birden çok kaynaktan toplanan verileri birleştirin ve başkalarıyla paylaşın. Çok bileşenli uygulamalar ve takım odasında sürekli görüntüleme için idealdir. |![Pano örneği](./media/app-insights-overview/dashboard-tn.png) |
| [**Canlı Ölçüm Akışı**](app-insights-live-stream.md)<br/>Yeni bir derleme dağıttığınızda, her şeyin beklendiği gibi çalıştığından emin olmak için bu neredeyse gerçek zamanlı performans göstergelerini izleyin. |![Canlı ölçüm örneği](./media/app-insights-overview/live-metrics-tn.png) |
| [**Analiz**](app-insights-analytics.md)<br/>Bu güçlü sorgulama dilini kullanarak uygulamanızın performansı ve kullanımıyla ilgili zor soruları yanıtlayın. |![Analiz örneği](./media/app-insights-overview/analytics-tn.png) |
| [**Visual Studio**](app-insights-visual-studio.md)<br/>Koddaki performans verilerini görün. Yığın izlemelerinden koda gidin.|![Visual studio](./media/app-insights-overview/visual-studio-tn.png) |
| [**Anlık görüntü hata ayıklayıcısı**](app-insights-snapshot-debugger.md)<br/>Dinamik işlemlerden örneklenen anlık görüntülerdeki hataları parametre değerleriyle ayıklayın.|![Visual studio](./media/app-insights-overview/snapshot.png) |
| [**Power BI**](app-insights-export-power-bi.md)<br/>Kullanım ölçümlerini diğer iş zekası verileriyle tümleştirin.| ![Power BI](./media/app-insights-overview/power-bi.png)|
| [**REST API**](https://dev.applicationinsights.io/)<br/>Ölçümleriniz ve ham verileriniz üzerinde sorgu çalıştırmak için kod yazın.| ![REST API](./media/app-insights-overview/rest-tn.png) |
| [**Sürekli dışarı aktarma**](app-insights-export-telemetry.md)<br/>Ham verilerin ulaşır ulaşmaz toplu olarak depolamaya aktarılması. |![Dışarı Aktarma](./media/app-insights-overview/export-tn.png) |

## <a name="how-do-i-use-application-insights"></a>Application Insights’ı nasıl kullanabilirim?

### <a name="monitor"></a>İzleme
Application Insights’ı uygulamanıza yükleyin, [kullanılabilirlik web testleri](app-insights-monitor-web-app-availability.md) ayarlayın ve:

* Yük ve yanıt verme hızının yanı sıra bağımlılıklarınızın, sayfa yüklemelerinizin ve AJAX çağrılarınızın performansını izlemek amacıyla takım odanız için bir [pano](app-insights-dashboards.md) ayarlayın.
* En yavaş ve en çok başarısız olan isteklerin hangileri olduğunu keşfedin.
* Yeni bir sürüm dağıttığınızda [Canlı Akış](app-insights-live-stream.md)’ı izleyerek herhangi bir performans düşüşünü anında görün.

### <a name="detect-diagnose"></a>Algılama, Tanılama
Bir uyarı aldığınızda veya bir sorun bulduğunuzda:

* Bu durumdan kaç kullanıcının etkilendiğini değerlendirin.
* Hatalar ile özel durumlar, bağımlılık çağrıları ve izlemeler arasında bağıntı kurun.
* Profil oluşturucuyu, anlık görüntüleri, yığın dökümlerini ve izleme günlüklerini inceleyin.

### <a name="build-measure-learn"></a>Oluşturma, Ölçme, Öğrenme
Dağıttığınız her yeni özelliğin [ne kadar etkili olduğunu ölçün](app-insights-usage-overview.md).

* Müşterilerin yeni kullanıcı arabirimini veya iş özelliklerini nasıl kullandığını ölçmeyi planlayın.
* Kodunuza özel telemetri yazın.
* Bir sonraki geliştirme döngüsünü telemetrinizden edindiğiniz somut kanıtlara dayandırın.

## <a name="get-started"></a>Başlarken
Application Insights, Microsoft Azure’da barındırılan birçok hizmetten biridir ve telemetri verileri analiz edilip sunulmak üzere buraya gönderilir. Bu nedenle, başka bir işlem yapmadan önce bir [Microsoft Azure](http://azure.com) aboneliğinizin olması gerekir. Kaydolmak ücretsizdir ve Application Insights’ın temel [fiyatlandırma planını](https://azure.microsoft.com/pricing/details/application-insights/) seçerseniz, uygulamanız önemli bir kullanım oranına ulaşana kadar ücret ödemezsiniz. Kuruluşunuzun zaten aboneliği varsa, Microsoft hesabınızı bu aboneliğe eklettirebilirsiniz.

Hizmeti kullanmaya başlamanın birkaç yolu vardır. Sizin için en uygun yöntemi kullanarak başlayın. Diğerlerini daha sonra ekleyebilirsiniz.

* **Çalışma zamanında: Sunucuda web uygulamanızı izleyin.** Kodda herhangi bir güncelleştirme yapmaktan kaçınır. Sunucunuza yönetici erişiminizin olması gerekir.
  * [**Şirket içinde veya bir VM’de IIS**](app-insights-monitor-performance-live-website-now.md)
  * [**Azure web uygulaması veya VM**](app-insights-monitor-performance-live-website-now.md)
  * [**J2EE**](app-insights-java-live.md)
* **Geliştirme zamanında: Application Insights’ı kodunuza ekleyin.** Özel telemetri yazmanızın yanı sıra arka uç ve masaüstü uygulamalarını izlemenize imkan tanır.
  * [Visual Studio](app-insights-asp-net.md) 2013 güncelleştirme 2 veya sonraki bir sürüm.
  * [Eclipse](app-insights-java-eclipse.md)’te veya [diğer araçlarda](app-insights-java-get-started.md) Java
  * [Node.js](app-insights-nodejs.md)
  * [Diğer platformlar](app-insights-platforms.md)
* Sayfa görütüleme, AJAX ve diğer istemci tarafı telemetri verileri bakımından **[web sayfalarınızı izleyin](app-insights-javascript.md)**.
* Visual Studio App Center ile tümleştirerek **[mobil uygulama kullanımını çözümleyin](app-insights-mobile-center-quickstart.md)**.
* **[Kullanılabilirlik testleri](app-insights-monitor-web-app-availability.md)**: Sunucularımızdan web sitenize düzenli aralıklarla ping gönderin.


## <a name="next-steps"></a>Sonraki adımlar
Çalışma zamanında şunlarla kullanmaya başlayın:

* [IIS sunucusu](app-insights-monitor-performance-live-website-now.md)
* [J2EE sunucusu](app-insights-java-live.md)

Geliştirme zamanında şunlarla kullanmaya başlayın:

* [ASP.NET](app-insights-asp-net.md)
* [Java](app-insights-java-get-started.md)
* [Node.js](app-insights-nodejs.md)

## <a name="support-and-feedback"></a>Destek ve geri bildirim
* Sorular ve Sorunlar:
  * [Sorun giderme][qna]
  * [MSDN Forumu](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=ApplicationInsights)
  * [StackOverflow](http://stackoverflow.com/questions/tagged/ms-application-insights)
* Önerileriniz:
  * [UserVoice](https://visualstudio.uservoice.com/forums/357324)
* Blog:
  * [Application Insights blogu](https://azure.microsoft.com/blog/tag/application-insights)

## <a name="videos"></a>Videolar

[![Animasyonlu giriş](./media/app-insights-overview/video-front-1.png)](https://www.youtube.com/watch?v=fX2NtGrh-Y0)

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

<!--Link references-->

[android]: https://github.com/Microsoft/ApplicationInsights-Android
[azure]: ../insights-perf-analytics.md
[client]: app-insights-javascript.md
[desktop]: app-insights-windows-desktop.md
[detect]: app-insights-detect-triage-diagnose.md
[greenbrown]: app-insights-asp-net.md
[ios]: https://github.com/Microsoft/ApplicationInsights-iOS
[java]: app-insights-java-get-started.md
[knowUsers]: app-insights-web-track-usage.md
[platforms]: app-insights-platforms.md
[portal]: http://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
