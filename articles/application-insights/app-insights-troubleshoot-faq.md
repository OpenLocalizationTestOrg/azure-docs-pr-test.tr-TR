---
title: "aaaAzure uygulama Öngörüler SSS | Microsoft Docs"
description: "Application Insights hakkında sık sorulan sorular."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0e3b103c-6e2a-4634-9e8c-8b85cf5e9c84
ms.service: application-insights
ms.workload: mobile
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: bwren
ms.openlocfilehash: e27ee9b7d040a04828a9892865a6681b83f94326
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-frequently-asked-questions"></a>Application Insights: Sık sorulan sorular

## <a name="configuration-problems"></a>Yapılandırma sorunları
*Sorun ayarı yaşıyorum my:*

* [.NET uygulaması](app-insights-asp-net-troubleshoot-no-data.md)
* [Zaten çalışan uygulama izleme](app-insights-monitor-performance-live-website-now.md#troubleshooting-runtime-configuration-of-application-insights)
* [Azure tanılama](app-insights-azure-diagnostics.md)
* [Java web uygulaması](app-insights-java-troubleshoot.md)

*Hiçbir veri sunucumdan alıyorum*

* [Set güvenlik duvarı özel durumlar](app-insights-ip-addresses.md)
* [ASP.NET sunucusu kurma](app-insights-monitor-performance-live-website-now.md)
* [Java sunucusunu ayarlama](app-insights-java-agent.md)

## <a name="can-i-use-application-insights-with-"></a>Application Insights ile kullanabilirim...?

* [Web uygulamaları IIS sunucusu - şirket içi veya VM](app-insights-asp-net.md)
* [Java web uygulamaları](app-insights-java-get-started.md)
* [Node.js uygulamaları](app-insights-nodejs.md)
* [Azure Web uygulamaları](app-insights-azure-web-apps.md)
* [Azure bulut Hizmetleri](app-insights-cloudservices.md)
* [Docker içinde çalışan uygulama sunucuları](app-insights-docker.md)
* [Tek sayfa web uygulamaları](app-insights-javascript.md)
* [SharePoint](app-insights-sharepoint.md)
* [Windows masaüstü uygulaması](app-insights-windows-desktop.md)
* [Diğer platformlar](app-insights-platforms.md)

## <a name="is-it-free"></a>Ücretsiz mi?

Evet, Deneysel için kullanın. Hello planı fiyatlandırma temel, uygulamanızı bir belirli indirimi veri her ay ücretsiz olarak gönderebilir. büyüklükte toocover geliştirme ve küçük bir kullanıcı sayısı için bir uygulama yayımlama Hello ücretsiz indirimi olur. Belirtilen miktarda veri birden çok uç tooprevent işlenmekte olan ayarlayabilirsiniz.

Telemetri daha büyük birimleri Gb hello tarafından ücretlendirilirsiniz. Bazı ipuçları çok sağladığımız[ücretlerinizi sınırlamak](app-insights-pricing.md).

Merhaba Kurumsal planı her web sunucusu düğümüne telemetri gönderen her gün için bir ücret doğurur. Toouse sürekli verme büyük bir ölçekte istiyorsanız uygundur.

[Plan fiyatlandırması okuma hello](https://azure.microsoft.com/pricing/details/application-insights/).

## <a name="how-much-is-it-costing"></a>Bu ne kadar maliyetlendirme?

* Açık hello **özellikleri + fiyatlandırma** Application Insights kaynağı sayfasında. Bir grafik son kullanım yoktur. İsterseniz, bir veri birimi cap ayarlayabilirsiniz.
* Açık hello [Azure faturalama dikey](https://portal.azure.com/#blade/Microsoft_Azure_Billing/BillingBlade/Overview) toosee faturalarınızı tüm kaynaklar arasında.

## <a name="q14"></a>Ne my projesinde Application Insights değiştirebilir?
Merhaba ayrıntıları proje hello türüne bağlıdır. Web uygulaması için:

* Bu dosyaları tooyour proje ekler:

  * Applicationınsights.config.
  * Ai.js
* Bu NuGet paketlerini yükler:

  * *Application Insights API'si* - hello API çekirdek
  * *Web uygulamaları için Application Insights API'si* -toosend telemetri hello sunucusundan kullanılan
  * *JavaScript uygulamaları için Application Insights API'si* -toosend telemetri hello istemciden kullanılan

    merhaba paketleri, bu derlemeler içerir:
  * Microsoft.ApplicationInsights
  * Microsoft.ApplicationInsights.Platform
* Öğeleri ekler:

  * Web.config
  * Packages.config
* (Yeni varsa yalnızca - projeleri, [Application Insights tooan varolan projeyi Ekle][start], toodo bu el ile sahip olduğunuz.) Kod parçacıkları hello istemci ve sunucu kodu tooinitialize ekler hello Application Insights kaynak kimliğiyle bunları Örneğin, bir MVC uygulamasında kodu hello ana sayfaya Views/Shared/_Layout.cshtml eklenir

## <a name="how-do-i-upgrade-from-older-sdk-versions"></a>Eski SDK sürümlerden nasıl yükseltme?
Merhaba bkz [sürüm notları](app-insights-release-notes.md) tooyour tür bir uygulama SDK'sı hello için uygun.

## <a name="update"></a>Proje için verileri gönderir hangi Azure kaynak nasıl değiştirebilir miyim?
Çözüm Gezgini'nde sağ `ApplicationInsights.config` ve **güncelleştirme Application Insights**. Azure'da hello, veri tooan mevcut veya yeni kaynak gönderebilirsiniz. Merhaba Güncelleştirme Sihirbazı'nı değişiklikleri izleme anahtarını hello sunucusu SDK verilerinizi burada gönderir belirler Applicationınsights.config içinde hello. "Tümünü Güncelleştir" kaldırmadıysanız web sayfalarınıza göründüğü hello anahtar da değiştirir.

## <a name="what-is-status-monitor"></a>Durum İzleyicisi nedir?

İçinde IIS web sunucusu toohelp kullanabileceğiniz bir masaüstü uygulamasının Application Insights web uygulamalarında yapılandırın. Telemetri toplamak değil: bir uygulama yapılandırırken değil durdurabilirsiniz. 

[Daha fazla bilgi edinin](app-insights-monitor-performance-live-website-now.md#questions).

## <a name="what-telemetry-is-collected-by-application-insights"></a>Hangi telemetri Application Insights tarafından toplanır?

Sunucu web uygulamaları:

* HTTP istekleri
* [Bağımlılıklar](app-insights-asp-net-dependencies.md). Çağrıları: SQL veritabanları; HTTP tooexternal hizmetlerini çağıran; Azure Cosmos DB, tablo, blob depolama ve sıra. 
* [Özel durumlar](app-insights-asp-net-exceptions.md) ve Yığın izlemeleri.
* [Performans sayaçları](app-insights-performance-counters.md) - kullanırsanız [Durum İzleyicisi](app-insights-monitor-performance-live-website-now.md), Azure monitoring(app-insights-azure-web-apps.md) veya hello [Application Insights collectd yazan](app-insights-java-collectd.md).
* [Özel olayları ve ölçümleri](app-insights-api-custom-events-metrics.md) , kod.
* [İzleme günlükleri](app-insights-asp-net-trace-logs.md) hello uygun Toplayıcı yapılandırırsanız.

Gelen [istemci web sayfaları](app-insights-javascript.md):

* [Sayfa görünümü sayar](app-insights-web-track-usage.md)
* [AJAX çağrıları](app-insights-asp-net-dependencies.md) çalışan komut dosyasından yapılan istekleri.
* Sayfa görünümü veri yükleme
* Kullanıcı ve oturum sayısı
* [Kimliği doğrulanmış kullanıcı kimlikleri](app-insights-api-custom-events-metrics.md#authenticated-users)

Bunları yapılandırırsanız, diğer kaynaklardan:

* [Azure tanılama](app-insights-azure-diagnostics.md)
* [Docker kapsayıcıları](app-insights-docker.md)
* [İçeri aktarma tooAnalytics tabloları](app-insights-analytics-import.md)
* [OMS (günlük analizi)](https://azure.microsoft.com/blog/omssolutionforappinsightspublicpreview/)
* [Logstash](app-insights-analytics-import.md)

## <a name="can-i-filter-out-or-modify-some-telemetry"></a>I filtrelemek veya birkaç telemetri değiştirmek için?

Evet, hello Server'da şunu yazabilirsiniz:

* Telemetri işlemci toofilter veya uygulamanızdan gönderilmeden önce özellikleri tooselected telemetri öğeleri ekleyebilirsiniz.
* Telemetri Başlatıcı tooadd özellikleri tooall öğeleri telemetri.

Daha fazla bilgi edinin [ASP.NET](app-insights-api-filtering-sampling.md) veya [Java](app-insights-java-filter-telemetry.md).

## <a name="how-are-city-country-and-other-geo-location-data-calculated"></a>Şehir, ülke ve diğer coğrafi konum verileri nasıl hesaplanır?

Biz hello IP adresini kullanarak hello web istemcisi (IPv4 veya IPv6) aramak [GeoLite2](http://dev.maxmind.com/geoip/geoip2/geolite2/).

* Tarayıcı telemetri: hello Gönderenin IP adresi toplarız.
* Sunucu telemetri: hello Application Insights modülü hello istemci IP adresi toplar. Varsa toplanmaz `X-Forwarded-For` ayarlanır.

Merhaba yapılandırabilirsiniz `ClientIpHeaderTelemetryInitializer` tootake hello bir IP adresinden farklı bir üstbilgi. Bazı sistemlerde, örneğin, bir proxy tarafından taşınırsa, çok yük dengeleyici veya CDN`X-Originating-IP`. [Daha fazla bilgi edinin](http://apmtips.com/blog/2016/07/05/client-ip-address/).

Yapabilecekleriniz [Power BI](app-insights-export-power-bi.md) toodisplay bir harita isteği telemetrinizi.


## <a name="data"></a>Ne kadar veri hello Portalı'nda tutulur? Güvenli mi?
Bir göz atalım [veri saklama ve gizlilik][data].

## <a name="might-personally-identifiable-information-pii-be-sent-in-hello-telemetry"></a>Kişisel olarak tanımlanabilir bilgileri (PII) hello telemetri gönderilmiş olabilir?

Bu, kodunuzu bu tür veri gönderiyorsa mümkün olur. Yığın izlemeleri değişkenlerde PII eklerseniz de oluşabilir. Geliştirme ekibiniz PII düzgün bir şekilde ele alınır risk değerlendirmeleri tooensure yürütmeniz gerekir. [Veri saklama ve gizlilik hakkında daha fazla bilgi edinmek](app-insights-data-retention-privacy.md).

Merhaba son sekizli hello istemci web adresinin her zaman too0 sonra alım hello portal tarafından ayarlanır.

## <a name="my-ikey-is-visible-in-my-web-page-source"></a>My iKey my web sayfası kaynağında görünür olur. 

* Bu çözümleri izleme yaygın bir uygulamadır.
* Bu, verilerinizi kullanılan toosteal olamaz.
* Bu, veri veya tetikleyici uyarılarınızı kullanılan tooskew olabilir.
* Biz herhangi bir müşteriye tür sorunları oluşturdu duymuş değil.

Size şunları yapabilir:

* (Application Insights kaynakları ayırın) iki ayrı iKeys istemci ve sunucu verileri için kullanın. Veya
* Sunucunuzda çalışan bir proxy yazma ve proxy üzerinden veri gönderme hello web istemcisi sahip.

## <a name="post"></a>Tanılama arama posta verileri nasıl görürüm?
Gönderme verisi otomatik olarak oturum yoktur, ancak bir TrackTrace çağrı kullanabilirsiniz: Merhaba ileti parametresinde hello verileri yerleştirme. Filtre uygulayamazsınız rağmen bu dize özellikleri hello sınırları daha uzun bir boyut sınırı vardır.

## <a name="should-i-use-single-or-multiple-application-insights-resources"></a>Tek veya birden çok Application Insights kaynağı kullanmalıyım?

Tek bir kaynak tüm hello bileşenleri ya da roller için tek bir iş sisteminde kullanın. Ayrı kaynaklar ve bağımsız uygulamalar geliştirme, test ve yayın sürümleri için kullanın.

* [Merhaba tartışma buraya bakın](app-insights-separate-resources.md)
* [Örnek - worker ve web rolleri sahip bulut hizmeti](app-insights-cloudservices.md)

## <a name="how-do-i-dynamically-change-hello-instrumentation-key"></a>Nasıl hello izleme anahtarını dinamik olarak değişir mi?

* [Burada tartışma](app-insights-separate-resources.md)
* [Örnek - worker ve web rolleri sahip bulut hizmeti](app-insights-cloudservices.md)

## <a name="what-are-hello-user-and-session-counts"></a>Sayıları hello kullanıcı ve oturum nelerdir?

* Merhaba JavaScript SDK'sı hello web istemcisi, tooidentify döndürmeyi kullanıcılar ve oturum tanımlama bilgisi toogroup etkinlikleri kullanıcı tanımlama bilgisi ayarlar.
* İstemci tarafı komut dosyası varsa, şunları yapabilirsiniz [hello sunucuda tanımlama bilgilerini ayarlama](http://apmtips.com/blog/2016/07/09/tracking-users-in-api-apps/).
* Farklı tarayıcılar veya içinde-özel/ıncognito gözatma kullanarak sitenizdeki bir gerçek kullanıcı kullanıyor veya farklı makinelerde sonra birden çok kez sayılacaktır varsa.
* tooidentify bir oturum açma kullanıcı makineler ve tarayıcılar arasında bir çağrı çok eklemek[setAuthenticatedUserContect()](app-insights-api-custom-events-metrics.md#authenticated-users).

## <a name="q17"></a>Her şeyi Application Insights etkinleştirdiniz mi?
| Görmeniz gerekir | Nasıl tooget, | İstediğiniz neden |
| --- | --- | --- |
| Kullanılabilirlik grafikleri |[Web testleri](app-insights-monitor-web-app-availability.md) |Web uygulamanız çalışıyor bildirin |
| Sunucu uygulaması perf: yanıt süreleri... |[Application Insights tooyour projesi eklemek](app-insights-asp-net.md) veya [sunucuda AI Durum İzleyicisi yükleme](app-insights-monitor-performance-live-website-now.md) (veya kendi kodunuzu çok yazma[izlemek bağımlılıkları](app-insights-api-custom-events-metrics.md#trackdependency)) |Performans sorunlarını Algıla |
| Bağımlılık telemetrisi |[Sunucuda AI Durum İzleyicisi yükleme](app-insights-monitor-performance-live-website-now.md) |Veritabanları veya diğer dış bileşenlere ile ilgili sorunları tanılamak |
| Özel durumlar Yığın izlemeleri Al |[Kodunuzda TrackException çağrıları ekleme](app-insights-asp-net-exceptions.md) (ancak bazı otomatik olarak bildirilen) |Algılamak ve tanılamak özel durumlar |
| Arama günlük izlemelerini |[Bir günlük bağdaştırıcısı ekleme](app-insights-asp-net-trace-logs.md) |Özel durumlar, performans sorunlarını tanılamanıza |
| İstemci kullanım temelleri: sayfa görünümleri, oturumlar,... |[Web sayfalarında JavaScript Başlatıcı](app-insights-javascript.md) |Kullanım analizi |
| İstemci özel ölçümleri |[Web sayfalarında izleme çağırır](app-insights-api-custom-events-metrics.md) |Kullanıcı deneyimini geliştirmek |
| Sunucu özel ölçümleri |[Sunucu izleme çağrıları](app-insights-api-custom-events-metrics.md) |İş zekası |

## <a name="why-are-hello-counts-in-search-and-metrics-charts-unequal"></a>Merhaba neden olan arama ve ölçümler grafiklerde eşit olmayan sayar?

[Örnekleme](app-insights-sampling.md) (istekleri, özel etkinlikler ve benzeri) uygulama toohello portalınızdan gerçekten gönderilip telemetri öğeleri hello sayısını azaltır. Aramada, aslında alınan öğe hello sayısı bakın. Etkinliklerin sayısını görüntüleyen ölçüm grafiklerde hello oluştu özgün olayların sayısının bakın. 

Transmmitted taşıyan olan her bir öğe bir `itemCount` öğenin kaç özgün olayları gösterir özelliğini temsil eder. tooobserve işleminde örnekleme, analizleri bu sorguyu çalıştırabilirsiniz:

```
    requests | summarize original_events = sum(itemCount), transmitted_events = count()
```


## <a name="automation"></a>Otomasyon

### <a name="configuring-application-insights"></a>Application Insights yapılandırma

Yapabilecekleriniz [PowerShell komut dosyaları yazmak](app-insights-powershell.md) Azure Kaynak Yöneticisi kullanarak:

* Oluşturun ve Application Insights kaynakları güncelleştirin.
* Plan fiyatlandırması hello ayarlayın.
* Merhaba izleme anahtarı edinme.
* Ölçüm uyarı ekleyin.
* Bir kullanılabilirlik test ekleyin.

Ölçüm Gezgini Raporu ayarlarken veya sürekli verme ayarlayın.

### <a name="querying-hello-telemetry"></a>Merhaba telemetri sorgulama

Kullanım hello [REST API](https://dev.applicationinsights.io/) toorun [Analytics](app-insights-analytics.md) sorgular.

## <a name="how-can-i-set-an-alert-on-an-event"></a>Bir olaya nasıl bir uyarı ayarlarım?

Azure uyarıları yalnızca üzerinde ölçümleridir. Bir değeri eşik, olay oluştuğunda yayılan özel bir ölçü oluşturun. Daha sonra bir uyarı hello ölçüm üzerinde ayarlayın. Unutmayın: her iki yönde; hello eşik hello ölçüm kestiği her bir bildirim alacaksınız bir bildirim hello hello başlangıç değeri yüksek veya düşük olup olsun ilk aşma kadar vermeyecektir; her zaman birkaç dakikalık bir gecikme yoktur.

## <a name="are-there-data-transfer-charges-between-an-azure-web-app-and-application-insights"></a>Bir Azure web uygulaması ve Application Insights arasında veri aktarımı ücretlerine var mı?

* Azure web uygulamanızın bir veri merkezinde barındırılıp barındırılmadığını Application Insights toplama bitiş noktası olduğunda, ücretsizdir. 
* Ana bilgisayar veri merkezinizde hiçbir toplama bitiş noktası olan sonra uygulamanızın telemetrisinde erişimliye [ücretleri giden Azure](https://azure.microsoft.com/pricing/details/bandwidth/).

Bu, Application Insights kaynağınıza burada barındırılan bağımlı değil. Yalnızca, bizim uç noktaları hello dağıtımını bağlıdır.

## <a name="can-i-send-telemetry-toohello-application-insights-portal"></a>Telemetri toohello Application Insights portalındaki gönderebilir miyim?

Bizim SDK'ları kullanın ve hello SDK API'si (app-insights-api-custom-events-metrics.md) kullanmanızı öneririz. Merhaba SDK çeşitli türevleri vardır [platformları](app-insights-platforms.md). Bu SDK'ları arabelleğe alma, sıkıştırma, azaltma, yeniden deneme ve benzeri işler. Ancak, hello [alım şema](https://github.com/Microsoft/ApplicationInsights-dotnet/tree/develop/Schema/PublicSchema) ve [endpoint Protokolü](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/EndpointSpecs/ENDPOINT-PROTOCOL.md) ortaktır.

## <a name="can-i-monitor-an-intranet-web-server"></a>Bir intranet web sunucusuna izleyebilir mi?

İki yöntem şunlardır:

### <a name="firewall-door"></a>Güvenlik Duvarı kapı

Web sunucusu toosend telemetri tooour uç noktaları https://dc.services.visualstudio.com:443 ve https://rt.services.visualstudio.com:443 izin verir. 

### <a name="proxy"></a>Ara sunucu

İntranetinizdeki Applicationınsights.Config'de ayarlayarak bu, sunucu tooa geçidinden trafiği yönlendirme:

```XML
<TelemetryChannel>
    <EndpointAddress>your gateway endpoint</EndpointAddress>
</TelemetryChannel>
```

Ağ geçidiniz hello trafiği toohttps://dc.services.visualstudio.com:443/v2/İzle rota

## <a name="can-i-run-availability-web-tests-on-an-intranet-server"></a>Kullanılabilirlik web testleri bir intranet sunucusunda çalıştırabilir miyim?

Bizim [web testleri](app-insights-monitor-web-app-availability.md) noktalarında Merhaba Dünya dağıtılan varlık çalıştırın. İki çözümü vardır:

* Güvenlik Duvarı kapı - isteklerine izin tooyour sunucudan [hello uzun ve web değiştirilebilir listesini test aracılarını](app-insights-ip-addresses.md).
* Kendi kod toosend düzenli istekleri tooyour sunucudan intranetinize içinde yazın. Bu amaç için Visual Studio web testleri çalıştırabilirsiniz. Merhaba tester hello sonuçları hello TrackAvailability() API kullanarak tooApplication Öngörüler gönderebilir.

## <a name="more-answers"></a>Daha fazla yanıtlar
* [Uygulama Öngörüler Forumu](https://social.msdn.microsoft.com/Forums/vstudio/en-US/home?forum=ApplicationInsights)

<!--Link references-->

[data]: app-insights-data-retention-privacy.md
[platforms]: app-insights-platforms.md
[start]: app-insights-overview.md
[windows]: app-insights-windows-get-started.md
