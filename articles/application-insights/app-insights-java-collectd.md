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
# <a name="collectd-linux-performance-metrics-in-application-insights"></a><span data-ttu-id="d1fac-103">collectd: Application Insights Linux performans ölçümlerini</span><span class="sxs-lookup"><span data-stu-id="d1fac-103">collectd: Linux performance metrics in Application Insights</span></span>


<span data-ttu-id="d1fac-104">tooexplore Linux sistem performans ölçümlerini [Application Insights](app-insights-overview.md), yükleme [collectd](http://collectd.org/), eklenti, Application Insights ile birlikte.</span><span class="sxs-lookup"><span data-stu-id="d1fac-104">tooexplore Linux system performance metrics in [Application Insights](app-insights-overview.md), install [collectd](http://collectd.org/), together with its Application Insights plug-in.</span></span> <span data-ttu-id="d1fac-105">Bu açık kaynak çözümü çeşitli sistem ve ağ istatistiklerini toplar.</span><span class="sxs-lookup"><span data-stu-id="d1fac-105">This open-source solution gathers various system and network statistics.</span></span>

<span data-ttu-id="d1fac-106">Genellikle, zaten varsa collectd kullanacağınız [Application Insights ile Java web hizmetiniz izlenmiş][java].</span><span class="sxs-lookup"><span data-stu-id="d1fac-106">Typically you'll use collectd if you have already [instrumented your Java web service with Application Insights][java].</span></span> <span data-ttu-id="d1fac-107">Daha fazla veri toohelp sağlar, tooenhance uygulamanızın performansını veya sorunları tanılamak.</span><span class="sxs-lookup"><span data-stu-id="d1fac-107">It gives you more data toohelp you tooenhance your app's performance or diagnose problems.</span></span> 

![Örnek grafikler](./media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a><span data-ttu-id="d1fac-109">İzleme anahtarı edinme</span><span class="sxs-lookup"><span data-stu-id="d1fac-109">Get your instrumentation key</span></span>
<span data-ttu-id="d1fac-110">Merhaba, [Microsoft Azure portal](https://portal.azure.com)açın hello [Application Insights](app-insights-overview.md) hello veri tooappear istediğiniz kaynak.</span><span class="sxs-lookup"><span data-stu-id="d1fac-110">In hello [Microsoft Azure portal](https://portal.azure.com), open hello [Application Insights](app-insights-overview.md) resource where you want hello data tooappear.</span></span> <span data-ttu-id="d1fac-111">(Veya [yeni bir kaynak oluşturmak](app-insights-create-new-resource.md).)</span><span class="sxs-lookup"><span data-stu-id="d1fac-111">(Or [create a new resource](app-insights-create-new-resource.md).)</span></span>

<span data-ttu-id="d1fac-112">Merhaba kaynağı tanımlayan hello izleme anahtarını bir kopyasını alın.</span><span class="sxs-lookup"><span data-stu-id="d1fac-112">Take a copy of hello instrumentation key, which identifies hello resource.</span></span>

![Tümüne Gözat, kaynağınızın açın ve ardından hello Essentials açılır, izleme anahtarı seçin ve Kopyala hello](./media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-hello-plug-in"></a><span data-ttu-id="d1fac-114">Collectd ve hello eklentisini yükleme</span><span class="sxs-lookup"><span data-stu-id="d1fac-114">Install collectd and hello plug-in</span></span>
<span data-ttu-id="d1fac-115">Linux sunucusu makineleri üzerinde:</span><span class="sxs-lookup"><span data-stu-id="d1fac-115">On your Linux server machines:</span></span>

1. <span data-ttu-id="d1fac-116">Yükleme [collectd](http://collectd.org/) sürüm 5.4.0 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="d1fac-116">Install [collectd](http://collectd.org/) version 5.4.0 or later.</span></span>
2. <span data-ttu-id="d1fac-117">Merhaba karşıdan [Application Insights collectd yazıcı eklentisi](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="d1fac-117">Download hello [Application Insights collectd writer plugin](https://aka.ms/aijavasdk).</span></span> <span data-ttu-id="d1fac-118">Merhaba sürüm numarasını not edin.</span><span class="sxs-lookup"><span data-stu-id="d1fac-118">Note hello version number.</span></span>
3. <span data-ttu-id="d1fac-119">Merhaba eklentisi JAR kopyalama içine `/usr/share/collectd/java`.</span><span class="sxs-lookup"><span data-stu-id="d1fac-119">Copy hello plugin JAR into `/usr/share/collectd/java`.</span></span>
4. <span data-ttu-id="d1fac-120">Düzen `/etc/collectd/collectd.conf`:</span><span class="sxs-lookup"><span data-stu-id="d1fac-120">Edit `/etc/collectd/collectd.conf`:</span></span>
   * <span data-ttu-id="d1fac-121">Emin [Java eklentisi hello](https://collectd.org/wiki/index.php/Plugin:Java) etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="d1fac-121">Ensure that [hello Java plugin](https://collectd.org/wiki/index.php/Plugin:Java) is enabled.</span></span>
   * <span data-ttu-id="d1fac-122">Merhaba JVMArg JAR aşağıdaki hello java.class.path tooinclude hello güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d1fac-122">Update hello JVMArg for hello java.class.path tooinclude hello following JAR.</span></span> <span data-ttu-id="d1fac-123">Karşıdan yüklediğiniz bir güncelleştirme hello sürüm numarası toomatch hello:</span><span class="sxs-lookup"><span data-stu-id="d1fac-123">Update hello version number toomatch hello one you downloaded:</span></span>
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * <span data-ttu-id="d1fac-124">Merhaba izleme anahtarı, kaynaktan kullanarak bu parçacığını ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d1fac-124">Add this snippet, using hello Instrumentation Key from your resource:</span></span>

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

<span data-ttu-id="d1fac-125">Örnek bir yapılandırma dosyası parçası şöyledir:</span><span class="sxs-lookup"><span data-stu-id="d1fac-125">Here's part of a sample configuration file:</span></span>

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

<span data-ttu-id="d1fac-126">Diğer yapılandırma [collectd eklentileri](https://collectd.org/wiki/index.php/Table_of_Plugins), hangi çeşitli verilerini toplayabilir farklı kaynaklardan.</span><span class="sxs-lookup"><span data-stu-id="d1fac-126">Configure other [collectd plugins](https://collectd.org/wiki/index.php/Table_of_Plugins), which can collect various data from different sources.</span></span>

<span data-ttu-id="d1fac-127">Tooits göre collectd yeniden [el ile](https://collectd.org/wiki/index.php/First_steps).</span><span class="sxs-lookup"><span data-stu-id="d1fac-127">Restart collectd according tooits [manual](https://collectd.org/wiki/index.php/First_steps).</span></span>

## <a name="view-hello-data-in-application-insights"></a><span data-ttu-id="d1fac-128">Görünüm hello verilerini Application ınsights'ta</span><span class="sxs-lookup"><span data-stu-id="d1fac-128">View hello data in Application Insights</span></span>
<span data-ttu-id="d1fac-129">Application Insights kaynağınıza açmak [ölçüm Gezgini ve grafikler ekleyin][metrics], hello ölçümleri seçerek hello özel kategorisinden toosee istiyor.</span><span class="sxs-lookup"><span data-stu-id="d1fac-129">In your Application Insights resource, open [Metrics Explorer and add charts][metrics], selecting hello metrics you want toosee from hello Custom category.</span></span>

![](./media/app-insights-java-collectd/result.png)

<span data-ttu-id="d1fac-130">Varsayılan olarak, hello ölçümleri hello ölçümleri toplanmış olan tüm ana bilgisayar makine genelinde toplanır.</span><span class="sxs-lookup"><span data-stu-id="d1fac-130">By default, hello metrics are aggregated across all host machines from which hello metrics were collected.</span></span> <span data-ttu-id="d1fac-131">tooview hello ölçümleri hello grafik ayrıntıları dikey penceresinde, ana bilgisayar başına gruplandırma'yı açın ve ardından CollectD ana bilgisayar tarafından toogroup seçin.</span><span class="sxs-lookup"><span data-stu-id="d1fac-131">tooview hello metrics per host, in hello Chart details blade, turn on Grouping and then choose toogroup by CollectD-Host.</span></span>

## <a name="tooexclude-upload-of-specific-statistics"></a><span data-ttu-id="d1fac-132">belirli istatistik tooexclude karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="d1fac-132">tooexclude upload of specific statistics</span></span>
<span data-ttu-id="d1fac-133">Varsayılan olarak, tüm etkin hello collectd tarafından toplanan tüm hello veri 'eklentileri okuma' hello Application Insights eklentisiyle gönderir.</span><span class="sxs-lookup"><span data-stu-id="d1fac-133">By default, hello Application Insights plugin sends all hello data collected by all hello enabled collectd 'read' plugins.</span></span> 

<span data-ttu-id="d1fac-134">belirli eklentileri veya veri kaynaklarının veri tooexclude:</span><span class="sxs-lookup"><span data-stu-id="d1fac-134">tooexclude data from specific plugins or data sources:</span></span>

* <span data-ttu-id="d1fac-135">Merhaba yapılandırma dosyasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="d1fac-135">Edit hello configuration file.</span></span> 
* <span data-ttu-id="d1fac-136">İçinde `<Plugin ApplicationInsightsWriter>`, böyle yönerge satırları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d1fac-136">In `<Plugin ApplicationInsightsWriter>`, add directive lines like this:</span></span>

| <span data-ttu-id="d1fac-137">Yönergesi</span><span class="sxs-lookup"><span data-stu-id="d1fac-137">Directive</span></span> | <span data-ttu-id="d1fac-138">Etki</span><span class="sxs-lookup"><span data-stu-id="d1fac-138">Effect</span></span> |
| --- | --- |
| `Exclude disk` |<span data-ttu-id="d1fac-139">Merhaba tarafından toplanan tüm veriler hariç `disk` eklentisi</span><span class="sxs-lookup"><span data-stu-id="d1fac-139">Exclude all data collected by hello `disk` plugin</span></span> |
| `Exclude disk:read,write` |<span data-ttu-id="d1fac-140">Adlı hello kaynaklarını Dışla `read` ve `write` hello gelen `disk` eklentisi.</span><span class="sxs-lookup"><span data-stu-id="d1fac-140">Exclude hello sources named `read` and `write` from hello `disk` plugin.</span></span> |

<span data-ttu-id="d1fac-141">Bir satır başı karakteri ile ayrı yönergeleri.</span><span class="sxs-lookup"><span data-stu-id="d1fac-141">Separate directives with a newline.</span></span>

## <a name="problems"></a><span data-ttu-id="d1fac-142">Sorunlarınız mı var?</span><span class="sxs-lookup"><span data-stu-id="d1fac-142">Problems?</span></span>
<span data-ttu-id="d1fac-143">*Veri hello portalında görmüyorum*</span><span class="sxs-lookup"><span data-stu-id="d1fac-143">*I don't see data in hello portal*</span></span>

* <span data-ttu-id="d1fac-144">Açık [arama] [ diagnostic] hello ham olayları geldiyseniz toosee.</span><span class="sxs-lookup"><span data-stu-id="d1fac-144">Open [Search][diagnostic] toosee if hello raw events have arrived.</span></span> <span data-ttu-id="d1fac-145">Bazen uzun tooappear ölçümleri Explorer'da aldıkları.</span><span class="sxs-lookup"><span data-stu-id="d1fac-145">Sometimes they take longer tooappear in metrics explorer.</span></span>
* <span data-ttu-id="d1fac-146">Çok gerekebilecek[ayarlamak giden veriler için güvenlik duvarı özel durumlar](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="d1fac-146">You might need too[set firewall exceptions for outgoing data](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="d1fac-147">Merhaba Application Insights eklentisiyle izlemeyi etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="d1fac-147">Enable tracing in hello Application Insights plugin.</span></span> <span data-ttu-id="d1fac-148">İçinde bu satırı ekleyin `<Plugin ApplicationInsightsWriter>`:</span><span class="sxs-lookup"><span data-stu-id="d1fac-148">Add this line within `<Plugin ApplicationInsightsWriter>`:</span></span>
  * `SDKLogger true`
* <span data-ttu-id="d1fac-149">Bir Terminali açın ve raporlama herhangi bir sorunla ayrıntılı modda toosee collectd Başlat:</span><span class="sxs-lookup"><span data-stu-id="d1fac-149">Open a terminal and start collectd in verbose mode, toosee any issues it is reporting:</span></span>
  * `sudo collectd -f`

## <a name="known-issue"></a><span data-ttu-id="d1fac-150">Bilinen bir sorun</span><span class="sxs-lookup"><span data-stu-id="d1fac-150">Known issue</span></span>

<span data-ttu-id="d1fac-151">Merhaba Öngörüler uygulama yazma eklentisi belirli okuma eklentileri ile uyumlu değil.</span><span class="sxs-lookup"><span data-stu-id="d1fac-151">hello Application Insights Write plugin is incompatible with certain Read plugins.</span></span> <span data-ttu-id="d1fac-152">Bazı eklentiler bazen "NaN burada hello Application Insights eklentisiyle kayan noktalı sayı bekliyor" gönderin.</span><span class="sxs-lookup"><span data-stu-id="d1fac-152">Some plugins sometimes send "NaN" where hello Application Insights plugin expects a floating-point number.</span></span>

<span data-ttu-id="d1fac-153">Belirti: Merhaba collectd günlüğü "AI:... dahil hataları gösterir. SyntaxError: beklenmeyen bir belirteç N ".</span><span class="sxs-lookup"><span data-stu-id="d1fac-153">Symptom: hello collectd log shows errors that include "AI: ... SyntaxError: Unexpected token N".</span></span>

<span data-ttu-id="d1fac-154">Geçici çözüm: hello sorun yazma eklentileri tarafından toplanan verileri dışlayın.</span><span class="sxs-lookup"><span data-stu-id="d1fac-154">Workaround: Exclude data collected by hello problem Write plugins.</span></span> 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md


