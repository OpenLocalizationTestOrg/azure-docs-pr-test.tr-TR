---
title: "Java web uygulaması performans Linux - Azure aaaMonitor | Microsoft Docs"
description: "Uygulama izleme için Application Insights performans hello CollectD eklentisi ile Java Web sitenizin genişletilmiş."
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 40c68f45-197a-4624-bf89-541eb7323002
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: bwren
ms.openlocfilehash: f783e8607a83b2b43f67d3a2fc20f100aa2f75ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="collectd-linux-performance-metrics-in-application-insights"></a>collectd: Application Insights Linux performans ölçümlerini


tooexplore Linux sistem performans ölçümlerini [Application Insights](app-insights-overview.md), yükleme [collectd](http://collectd.org/), eklenti, Application Insights ile birlikte. Bu açık kaynak çözümü çeşitli sistem ve ağ istatistiklerini toplar.

Genellikle, zaten varsa collectd kullanacağınız [Application Insights ile Java web hizmetiniz izlenmiş][java]. Daha fazla veri toohelp sağlar, tooenhance uygulamanızın performansını veya sorunları tanılamak. 

![Örnek grafikler](./media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a>İzleme anahtarı edinme
Merhaba, [Microsoft Azure portal](https://portal.azure.com)açın hello [Application Insights](app-insights-overview.md) hello veri tooappear istediğiniz kaynak. (Veya [yeni bir kaynak oluşturmak](app-insights-create-new-resource.md).)

Merhaba kaynağı tanımlayan hello izleme anahtarını bir kopyasını alın.

![Tümüne Gözat, kaynağınızın açın ve ardından hello Essentials açılır, izleme anahtarı seçin ve Kopyala hello](./media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-hello-plug-in"></a>Collectd ve hello eklentisini yükleme
Linux sunucusu makineleri üzerinde:

1. Yükleme [collectd](http://collectd.org/) sürüm 5.4.0 veya sonraki bir sürümü.
2. Merhaba karşıdan [Application Insights collectd yazıcı eklentisi](https://aka.ms/aijavasdk). Merhaba sürüm numarasını not edin.
3. Merhaba eklentisi JAR kopyalama içine `/usr/share/collectd/java`.
4. Düzen `/etc/collectd/collectd.conf`:
   * Emin [Java eklentisi hello](https://collectd.org/wiki/index.php/Plugin:Java) etkinleştirilir.
   * Merhaba JVMArg JAR aşağıdaki hello java.class.path tooinclude hello güncelleştirin. Karşıdan yüklediğiniz bir güncelleştirme hello sürüm numarası toomatch hello:
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * Merhaba izleme anahtarı, kaynaktan kullanarak bu parçacığını ekleyin:

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

Örnek bir yapılandırma dosyası parçası şöyledir:

```XML

    ...
    # collectd plugins
    LoadPlugin cpu
    LoadPlugin disk
    LoadPlugin load
    ...

    # Enable Java Plugin
    LoadPlugin "java"

    # Configure Java Plugin
    <Plugin "java">
      JVMArg "-verbose:jni"
      JVMArg "-Djava.class.path=/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar:/usr/share/collectd/java/collectd-api.jar"

      # Enabling Application Insights plugin
      LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"

      # Configuring Application Insights plugin
      <Plugin ApplicationInsightsWriter>
        InstrumentationKey "12345678-1234-1234-1234-123456781234"
      </Plugin>

      # Other plugin configurations ...
      ...
    </Plugin>
    ...
```

Diğer yapılandırma [collectd eklentileri](https://collectd.org/wiki/index.php/Table_of_Plugins), hangi çeşitli verilerini toplayabilir farklı kaynaklardan.

Tooits göre collectd yeniden [el ile](https://collectd.org/wiki/index.php/First_steps).

## <a name="view-hello-data-in-application-insights"></a>Görünüm hello verilerini Application ınsights'ta
Application Insights kaynağınıza açmak [ölçüm Gezgini ve grafikler ekleyin][metrics], hello ölçümleri seçerek hello özel kategorisinden toosee istiyor.

![](./media/app-insights-java-collectd/result.png)

Varsayılan olarak, hello ölçümleri hello ölçümleri toplanmış olan tüm ana bilgisayar makine genelinde toplanır. tooview hello ölçümleri hello grafik ayrıntıları dikey penceresinde, ana bilgisayar başına gruplandırma'yı açın ve ardından CollectD ana bilgisayar tarafından toogroup seçin.

## <a name="tooexclude-upload-of-specific-statistics"></a>belirli istatistik tooexclude karşıya yükleme
Varsayılan olarak, tüm etkin hello collectd tarafından toplanan tüm hello veri 'eklentileri okuma' hello Application Insights eklentisiyle gönderir. 

belirli eklentileri veya veri kaynaklarının veri tooexclude:

* Merhaba yapılandırma dosyasını düzenleyin. 
* İçinde `<Plugin ApplicationInsightsWriter>`, böyle yönerge satırları ekleyin:

| Yönergesi | Etki |
| --- | --- |
| `Exclude disk` |Merhaba tarafından toplanan tüm veriler hariç `disk` eklentisi |
| `Exclude disk:read,write` |Adlı hello kaynaklarını Dışla `read` ve `write` hello gelen `disk` eklentisi. |

Bir satır başı karakteri ile ayrı yönergeleri.

## <a name="problems"></a>Sorunlarınız mı var?
*Veri hello portalında görmüyorum*

* Açık [arama] [ diagnostic] hello ham olayları geldiyseniz toosee. Bazen uzun tooappear ölçümleri Explorer'da aldıkları.
* Çok gerekebilecek[ayarlamak giden veriler için güvenlik duvarı özel durumlar](app-insights-ip-addresses.md)
* Merhaba Application Insights eklentisiyle izlemeyi etkinleştirin. İçinde bu satırı ekleyin `<Plugin ApplicationInsightsWriter>`:
  * `SDKLogger true`
* Bir Terminali açın ve raporlama herhangi bir sorunla ayrıntılı modda toosee collectd Başlat:
  * `sudo collectd -f`

## <a name="known-issue"></a>Bilinen bir sorun

Merhaba Öngörüler uygulama yazma eklentisi belirli okuma eklentileri ile uyumlu değil. Bazı eklentiler bazen "NaN burada hello Application Insights eklentisiyle kayan noktalı sayı bekliyor" gönderin.

Belirti: Merhaba collectd günlüğü "AI:... dahil hataları gösterir. SyntaxError: beklenmeyen bir belirteç N ".

Geçici çözüm: hello sorun yazma eklentileri tarafından toplanan verileri dışlayın. 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md


