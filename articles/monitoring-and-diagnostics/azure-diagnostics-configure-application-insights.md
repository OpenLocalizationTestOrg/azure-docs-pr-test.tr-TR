---
title: "aaaConfigure Azure tanılama toosend veri tooApplication Insights | Microsoft Docs"
description: "Hello Azure tanılama genel yapılandırması toosend veri tooApplication Öngörüler güncelleştirin."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: f9e12c3e-c307-435e-a149-ef0fef20513a
ms.service: monitoring-and-diagnostics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/19/2016
ms.author: robb
ms.openlocfilehash: 7c36f29da8fdc12fa58c17458348a311b900b0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-tooapplication-insights"></a><span data-ttu-id="85887-103">Bulut hizmeti, sanal makine ya da Service Fabric tanılama veri tooApplication Öngörüler Gönder</span><span class="sxs-lookup"><span data-stu-id="85887-103">Send Cloud Service, Virtual Machine, or Service Fabric diagnostic data tooApplication Insights</span></span>
<span data-ttu-id="85887-104">Bulut Hizmetleri, sanal makineler, sanal makine ölçek kümeleri ve Service Fabric tüm hello Azure tanılama uzantısını toocollect verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="85887-104">Cloud services, Virtual Machines, Virtual Machine Scale Sets and Service Fabric all use hello Azure Diagnostics extension toocollect data.</span></span>  <span data-ttu-id="85887-105">Azure Tanılama verileri tooAzure depolama tabloları gönderir.</span><span class="sxs-lookup"><span data-stu-id="85887-105">Azure diagnostics sends data tooAzure Storage tables.</span></span>  <span data-ttu-id="85887-106">Ancak, ayrıca tüm kanal veya bir alt kümesini hello veri tooother konumları 1.5 veya daha sonra Azure tanılama uzantısını kullanarak erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85887-106">However, you can also pipe all or a subset of hello data tooother locations using Azure Diagnostics extension 1.5 or later.</span></span>

<span data-ttu-id="85887-107">Bu makalede, Azure tanılama uzantısını tooApplication Öngörüler toosend verileri nasıl hello açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="85887-107">This article describes how toosend data from hello Azure Diagnostics extension tooApplication Insights.</span></span>

## <a name="diagnostics-configuration-explained"></a><span data-ttu-id="85887-108">Açıklanan tanılama yapılandırması</span><span class="sxs-lookup"><span data-stu-id="85887-108">Diagnostics configuration explained</span></span>
<span data-ttu-id="85887-109">Tanılama verileri nerede Gönder ek konumlarının Azure tanılama sunulan uzantısı 1.5 havuzlarını hello.</span><span class="sxs-lookup"><span data-stu-id="85887-109">hello Azure diagnostics extension 1.5 introduced sinks, which are additional locations where you can send diagnostic data.</span></span>

<span data-ttu-id="85887-110">Bir havuz örnek yapılandırma Application Insights için:</span><span class="sxs-lookup"><span data-stu-id="85887-110">Example configuration of a sink for Application Insights:</span></span>

```XML
<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "ApplicationInsights",
            "ApplicationInsights": "{Insert InstrumentationKey}",
            "Channels": {
                "Channel": [
                    {
                        "logLevel": "Error",
                        "name": "MyTopDiagData"
                    },
                    {
                        "logLevel": "Error",
                        "name": "MyLogData"
                    }
                ]
            }
        }
    ]
}
```
- <span data-ttu-id="85887-111">Merhaba **havuz** *adı* hello havuzu benzersiz olarak tanımlayan bir dize değeri bir özniteliktir.</span><span class="sxs-lookup"><span data-stu-id="85887-111">hello **Sink** *name* attribute is a string value that uniquely identifies hello sink.</span></span>

- <span data-ttu-id="85887-112">Merhaba **Applicationınsights** öğesi hello hello Azure Tanılama verileri nerede gönderilir uygulama Öngörüler kaynak izleme anahtarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="85887-112">hello **ApplicationInsights** element specifies instrumentation key of hello Application insights resource where hello Azure diagnostics data is sent.</span></span>
    - <span data-ttu-id="85887-113">Varolan bir Application Insights kaynağı sahip değilseniz, bkz: [yeni bir Application Insights kaynağı oluşturma](../application-insights/app-insights-create-new-resource.md) kaynak oluşturma ve hello izleme anahtarı alma hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="85887-113">If you don't have an existing Application Insights resource, see [Create a new Application Insights resource](../application-insights/app-insights-create-new-resource.md) for more information on creating a resource and getting hello instrumentation key.</span></span>
    - <span data-ttu-id="85887-114">Bir bulut hizmeti Azure SDK 2.8 ve daha sonra geliştiriyorsanız, bu izleme anahtarını otomatik olarak doldurulur.</span><span class="sxs-lookup"><span data-stu-id="85887-114">If you are developing a Cloud Service with Azure SDK 2.8 and later, this instrumentation key is automatically populated.</span></span> <span data-ttu-id="85887-115">Merhaba değeri hello üzerinde temel **appınsıghts_ınstrumentatıonkey** hello Cloud Service projesi paketleme, hizmet yapılandırma ayarı.</span><span class="sxs-lookup"><span data-stu-id="85887-115">hello value is based on hello **APPINSIGHTS_INSTRUMENTATIONKEY** service configuration setting when packaging hello Cloud Service project.</span></span> <span data-ttu-id="85887-116">Bkz: [bulut hizmeti kullanım Application Insights'a Azure tanılama tootroubleshoot sorunları](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span><span class="sxs-lookup"><span data-stu-id="85887-116">See [Use Application Insights with Azure Diagnostics tootroubleshoot Cloud Service issues](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span></span>

- <span data-ttu-id="85887-117">Merhaba **kanalları** öğesi içeren bir veya daha fazla **kanal** öğeleri.</span><span class="sxs-lookup"><span data-stu-id="85887-117">hello **Channels** element contains one or more **Channel** elements.</span></span>
    - <span data-ttu-id="85887-118">Merhaba *adı* özniteliği benzersiz olarak toothat kanal başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="85887-118">hello *name* attribute uniquely refers toothat channel.</span></span>
    - <span data-ttu-id="85887-119">Merhaba *loglevel* özniteliği kanal hello hello günlük düzeyi verir belirtmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="85887-119">hello *loglevel* attribute lets you specify hello log level that hello channel allows.</span></span> <span data-ttu-id="85887-120">Çoğu tooleast bilgi sırasına Hello kullanılabilir günlük düzeyleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="85887-120">hello available log levels in order of most tooleast information are:</span></span>
        - <span data-ttu-id="85887-121">Ayrıntılı</span><span class="sxs-lookup"><span data-stu-id="85887-121">Verbose</span></span>
        - <span data-ttu-id="85887-122">Bilgi</span><span class="sxs-lookup"><span data-stu-id="85887-122">Information</span></span>
        - <span data-ttu-id="85887-123">Uyarı</span><span class="sxs-lookup"><span data-stu-id="85887-123">Warning</span></span>
        - <span data-ttu-id="85887-124">Hata</span><span class="sxs-lookup"><span data-stu-id="85887-124">Error</span></span>
        - <span data-ttu-id="85887-125">Kritik</span><span class="sxs-lookup"><span data-stu-id="85887-125">Critical</span></span>

<span data-ttu-id="85887-126">Bir kanal bir filtre gibi davranır ve tooselect belirli günlük düzeyleri toosend toohello hedef havuz sağlar.</span><span class="sxs-lookup"><span data-stu-id="85887-126">A channel acts like a filter and allows you tooselect specific log levels toosend toohello target sink.</span></span> <span data-ttu-id="85887-127">Örneğin, ayrıntılı günlükleri toplamak ve toostorage Gönder ancak yalnızca hataları toohello havuz Gönder.</span><span class="sxs-lookup"><span data-stu-id="85887-127">For example, you could collect verbose logs and send them toostorage, but send only Errors toohello sink.</span></span>

<span data-ttu-id="85887-128">Merhaba aşağıdaki grafikte bu ilişkiyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="85887-128">hello following graphic shows this relationship.</span></span>

![Tanılama genel yapılandırması](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

<span data-ttu-id="85887-130">Grafiği aşağıdaki hello hello yapılandırma değerlerini ve nasıl çalıştığını özetler.</span><span class="sxs-lookup"><span data-stu-id="85887-130">hello following graphic summarizes hello configuration values and how they work.</span></span> <span data-ttu-id="85887-131">Merhaba hiyerarşideki farklı düzeylerde hello yapılandırmasında birden çok havuzlarını içerebilir.</span><span class="sxs-lookup"><span data-stu-id="85887-131">You can include multiple sinks in hello configuration at different levels in hello hierarchy.</span></span> <span data-ttu-id="85887-132">en üst düzeyinde hello Hello havuz genel ayar olarak davranır ve hello bir hello tek tek öğesi bir geçersiz kılma toothat genel ayar gibi davranır belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="85887-132">hello sink at hello top level acts as a global setting and hello one specified at hello individual element acts like an override toothat global setting.</span></span>

![Tanılama yapılandırması Application Insights ile iç havuzlar](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a><span data-ttu-id="85887-134">Tam havuz yapılandırma örneği</span><span class="sxs-lookup"><span data-stu-id="85887-134">Complete sink configuration example</span></span>
<span data-ttu-id="85887-135">İşte hello genel yapılandırmasının tam bir örnek dosya</span><span class="sxs-lookup"><span data-stu-id="85887-135">Here is a complete example of hello public configuration file that</span></span>
1. <span data-ttu-id="85887-136">tüm hataları tooApplication Öngörüler gönderir (Merhaba sırasında belirtilen **DiagnosticMonitorConfiguration** düğüm)</span><span class="sxs-lookup"><span data-stu-id="85887-136">sends all errors tooApplication Insights (specified at hello **DiagnosticMonitorConfiguration** node)</span></span>
2. <span data-ttu-id="85887-137">Ayrıca hello uygulama günlükleri için ayrıntılı düzeyi günlüklerini gönderir (Merhaba sırasında belirtilen **günlükleri** düğüm).</span><span class="sxs-lookup"><span data-stu-id="85887-137">also sends Verbose level logs for hello Application Logs (specified at hello **Logs** node).</span></span>

```XML
<WadCfg>
  <DiagnosticMonitorConfiguration overallQuotaInMB="4096"
       sinks="ApplicationInsights.MyTopDiagData"> <!-- All info below sent toothis channel -->
    <DiagnosticInfrastructureLogs />
    <PerformanceCounters>
      <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
    </PerformanceCounters>
    <WindowsEventLog scheduledTransferPeriod="PT1M">
      <DataSource name="Application!*" />
    </WindowsEventLog>
    <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose"
            sinks="ApplicationInsights.MyLogData"/> <!-- This specific info sent toothis channel -->
  </DiagnosticMonitorConfiguration>

<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
  </SinksConfig>
</WadCfg>
```
```JSON
"WadCfg": {
    "DiagnosticMonitorConfiguration": {
        "overallQuotaInMB": 4096,
        "sinks": "ApplicationInsights.MyTopDiagData", "_comment": "All info below sent toothis channel",
        "DiagnosticInfrastructureLogs": {
        },
        "PerformanceCounters": {
            "PerformanceCounterConfiguration": [
                {
                    "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                    "sampleRate": "PT3M"
                },
                {
                    "counterSpecifier": "\\Memory\\Available MBytes",
                    "sampleRate": "PT3M"
                }
            ]
        },
        "WindowsEventLog": {
            "scheduledTransferPeriod": "PT1M",
            "DataSource": [
                {
                    "name": "Application!*"
                }
            ]
        },
        "Logs": {
            "scheduledTransferPeriod": "PT1M",
            "scheduledTransferLogLevelFilter": "Verbose",
            "sinks": "ApplicationInsights.MyLogData", "_comment": "This specific info sent toothis channel"
        }
    },
    "SinksConfig": {
        "Sink": [
            {
                "name": "ApplicationInsights",
                "ApplicationInsights": "{Insert InstrumentationKey}",
                "Channels": {
                    "Channel": [
                        {
                            "logLevel": "Error",
                            "name": "MyTopDiagData"
                        },
                        {
                            "logLevel": "Verbose",
                            "name": "MyLogData"
                        }
                    ]
                }
            }
        ]
    }
}
```
<span data-ttu-id="85887-138">Merhaba önceki yapılandırmada satırlardan hello hello anlamları şu olabilir:</span><span class="sxs-lookup"><span data-stu-id="85887-138">In hello previous configuration, hello following lines have hello following meanings:</span></span>

### <a name="send-all-hello-data-that-is-being-collected-by-azure-diagnostics"></a><span data-ttu-id="85887-139">Azure tanılama tarafından toplanan tüm hello verileri gönder</span><span class="sxs-lookup"><span data-stu-id="85887-139">Send all hello data that is being collected by Azure diagnostics</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-toohello-application-insights-sink"></a><span data-ttu-id="85887-140">Yalnızca hata günlükleri toohello Application Insights havuz Gönder</span><span class="sxs-lookup"><span data-stu-id="85887-140">Send only error logs toohello Application Insights sink</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-tooapplication-insights"></a><span data-ttu-id="85887-141">Ayrıntılı uygulama tooApplication Öngörüler günlüklerini Gönder</span><span class="sxs-lookup"><span data-stu-id="85887-141">Send Verbose application logs tooApplication Insights</span></span>

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a><span data-ttu-id="85887-142">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="85887-142">Limitations</span></span>

- <span data-ttu-id="85887-143">**Kanallar yalnızca türü ve değil performans sayaçlarını günlüğe kaydeder.**</span><span class="sxs-lookup"><span data-stu-id="85887-143">**Channels only log type and not performance counters.**</span></span> <span data-ttu-id="85887-144">Bir performans sayacı öğesi ile bir kanal belirtirseniz, yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="85887-144">If you specify a channel with a performance counter element, it is ignored.</span></span>
- <span data-ttu-id="85887-145">**Merhaba günlük düzeyi için bir kanal tarafından Azure tanılama toplanmakta için hello günlük düzeyi aşamaz.**</span><span class="sxs-lookup"><span data-stu-id="85887-145">**hello log level for a channel cannot exceed hello log level for what is being collected by Azure diagnostics.**</span></span> <span data-ttu-id="85887-146">Örneğin, uygulama günlüğüne hataları hello günlükleri öğesindeki toplamak ve toosend ayrıntılı günlükleri toohello uygulama Insight havuz deneyin.</span><span class="sxs-lookup"><span data-stu-id="85887-146">For example, you cannot collect Application Log errors in hello Logs element and try toosend Verbose logs toohello Application Insight sink.</span></span> <span data-ttu-id="85887-147">Merhaba *scheduledTransferLogLevelFilter* özniteliği gerekir her zaman toplamak eşit veya hello günlükleri çok daha fazla günlükleri toosend tooa havuz çalışıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="85887-147">hello *scheduledTransferLogLevelFilter* attribute must always collect equal or more logs than hello logs you are trying toosend tooa sink.</span></span>
- <span data-ttu-id="85887-148">**Azure tanılama uzantısını tooApplication Insights tarafından toplanan blob verileri gönderemez.**</span><span class="sxs-lookup"><span data-stu-id="85887-148">**You cannot send blob data collected by Azure diagnostics extension tooApplication Insights.**</span></span> <span data-ttu-id="85887-149">Örneğin, hello altında belirtilen hiçbir şey *dizinleri* düğümü.</span><span class="sxs-lookup"><span data-stu-id="85887-149">For example, anything specified under hello *Directories* node.</span></span> <span data-ttu-id="85887-150">Merhaba gerçek kilitlenme dökümü kilitlenme dökümleri tooblob depolama gönderilir ve yalnızca kilitlenme döküm hello bir bildirim oluşturulan tooApplication Öngörüler gönderilir.</span><span class="sxs-lookup"><span data-stu-id="85887-150">For Crash Dumps hello actual crash dump is sent tooblob storage and only a notification that hello crash dump was generated is sent tooApplication Insights.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85887-151">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="85887-151">Next Steps</span></span>
* <span data-ttu-id="85887-152">Nasıl çok öğrenin[Azure tanılama bilgilerinizi görüntülemek](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) Application ınsights'ta.</span><span class="sxs-lookup"><span data-stu-id="85887-152">Learn how too[view your Azure diagnostics information](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) in Application Insights.</span></span>
* <span data-ttu-id="85887-153">Kullanım [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable hello uygulamanız için Azure tanılama uzantısını.</span><span class="sxs-lookup"><span data-stu-id="85887-153">Use [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable hello Azure diagnostics extension for your application.</span></span>
* <span data-ttu-id="85887-154">Kullanım [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable hello uygulamanız için Azure tanılama uzantısını</span><span class="sxs-lookup"><span data-stu-id="85887-154">Use [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable hello Azure diagnostics extension for your application</span></span>
